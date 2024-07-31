# обучающий код "Как парсить одну табличку на основании колонок другой таблички"

# загружаем наобходимые пакеты
library(tidyverse)
library(readxl)

# загружаем и чистим таблицу, из которой нужно отфильтровать необходимые значения
# допустим, в качестве таблицы у нас результат работы аннотации из eggnog'a
test_eggnog_output <- read_excel("C:/Users/test_eggnog_output.xlsx", col_names = F) %>% # тут пропиши свой путь
  filter(!grepl("#", ...1)) %>% # удаляем из первой колонки все, что содержит "#", так как у eggnog так обозначаются технические строки
  `colnames<-`(.[1, ]) %>% # строку с именами колонок делаем собственно именами колонок
  .[-1, ] # удаляем уже не нужную строку с именами, точка указывает что надо данные входа использовать

# загружаем две таблицы, в которых содержаться данные об интересующих нас генах
# данные об интересующих генах - это твои микро-базы данных, которые ты обычно составляешь самостоятельно, чтобы по ним искать
# в первой таблице, допустим, у нас колонки KEGG_ko и PFAMs (колонки которые есть в целевой таблице, в которой мы что-то ищем)
first_table_to_filter_by <- read_excel("C:/Users/first_table_to_filter_by.xlsx")
# во второй, допустим, у нас Preferred_name и Description (тоже есть в целевой таблице)
second_table_to_filter_by <- read_excel("C:/Users/second_table_to_filter_by.xlsx")

# теперь мы хотим оставить в "test_eggnog_output" только значения из колонок таблиц first_table_to_filter_by и second_table_to_filter_by

# самое простое решение - использовать функцию filter() в связке с оператором %in%

# этот код вытаскивает все строки из целевой таблицы, у которых значения колонки "KEGG_ko"  соответствуют таковым в первой таблице с интересующими тебя генами 
test_eggnog_output %>% 
  filter((KEGG_ko %in% first_table_to_filter_by$KEGG_ko))

# допустим, фильтровать надо не по одной колонке из первой таблицы, а по двум
# тогда добавляем логическое "ИЛИ" (обозначается символом "|") и дополнительный фильтр в код
test_eggnog_output %>% 
  filter((KEGG_ko %in% first_table_to_filter_by$KEGG_ko) |
         (PFAMs %in% first_table_to_filter_by$PFAMs)) # та же таблица, но вторая колонка

# теперь допустим, что надо фильтровать по двум отдельным табличкам
# тогда так -
test_eggnog_output %>% 
  filter((KEGG_ko %in% first_table_to_filter_by$KEGG_ko) |
         (PFAMs %in% first_table_to_filter_by$PFAMs) |
         (Preferred_name %in% second_table_to_filter_by$Preferred_name)| # тут мы уже фильтруем по колонке Preferred_name из таблицы second_table_to_filter_by
         (Description %in% second_table_to_filter_by$Description)) # а тут по Description из second_table_to_filter_by

# если нужно сначала отфильтровать по одной колонке, а потом фильтрат профильтровать по другой, тогда необходимые фильтры стоит применять последовательно
test_eggnog_output %>% 
  filter(KEGG_ko %in% first_table_to_filter_by$KEGG_ko) %>% # после выполнения этой фильтрующей функции в датасете остается шесть строк
  filter(Preferred_name %in% second_table_to_filter_by$Preferred_name) # после выполнения этой функции в таблице останется ноль строк, поскольку из шести оставшишхся на предыдущем этапе строк ни одна не содержит такие значения Preferred_name, какие есть в таблице second_table_to_filter_by

# если нужно фильтровать не списку конкретных значений, а по отдельным вещам или по шаблону, то можно пользоваться логическими операторами просто так или в комбинации с функцией grepl (но тогда надо прописывать нужные или наоборот ненужные вещи вручную)
test_eggnog_output %>% 
  filter(grepl("sulfur", Description)) %>% # оставить только те строки, у которых в колонке Description есть что угодно с sulfur
  filter(!grepl("nuoC", Preferred_name)) %>%  # логическое "НЕ", которое в R обозначается как "!", делает отрицательный фильтр из функции grepl, тут мы выкидываем все строки, где в колонке Preferred_name есть что угодно nuoC
  filter((grepl("Deltaproteobacteria", max_annot_lvl) | grepl("Epsilonproteobacteria", max_annot_lvl)) & grepl("NDH", Description)) %>% # логическое "И", оставляем только конкретные два таксона по колонке max_annot_lvl И только то, что содердит NDH в колонке Description
  filter(KEGG_ko != "ko:K00330") %>% # отрицательный фильтр который фильтрует не по шаблону, а по однозначному соответствию (несоответствию)
  filter(KEGG_ko == "ko:K00331") # положительный фильтр который фильтрует не по шаблону, а по однозначному соответствию
