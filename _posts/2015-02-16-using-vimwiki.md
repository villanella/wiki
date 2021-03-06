---
layout: post
title: "Использование Vimwiki для работы с сайтом на jekyll" 
date: 2015-02-17 00:03:05
categories: blog
tags: [tags for the post, is here]  
summary: удобный инструмент блоггинга 
---

## Vim + vimwiki + markdown + github + jekyll

Используем привычный инструмент ведения заметок [Vimwiki](http://www.vim.org/scripts/script.php?script_id=2226 "Vimwiki") в качестве markdown-редактора сайта на jekyll. 

##Преимущества подхода:

* быстрый доступ к локальному репозиторию;
* подсветка кода;
* полуавтоматическое написание названий.


### Настройка .vimrc

    let g:vimwiki_list = [{'path': '~/my_site/_posts',
                         \ 'syntax': 'markdown', 'ext': '.md',
                         \ 'diary_rel_path': ''}]

Длинный вариант для тех, у кого используется несколько vimwiki:

```
    let wiki_6 = {}
    let wiki_6.path = '~/my_site/_posts/'
    let wiki_6.index = 'main'
    let wiki_6.syntax = 'markdown'
    let wiki_6.ext = '.md'
    let wiki_6.diary_rel_path = ''
```

Указываем расположение локального репозитория с файлами публикаций, название индексного файла (факультативно), подсветку синтаксиса - markdown, нужное расширение. Последняя запись - местонахождение папки с дневниковыми записями, которое необходимо указать, если планируется использовать vimwiki-diary.

Далее настраиваем быструю вставку текущей даты по клавише F3 с помощью функции *strftime()*: 

```
" Entry Current Date
nnoremap <F3> "=strftime("%Y-%m-%d")<CR>P
inoremap <F3> <C-R>=strftime("%Y-%m-%d")<CR>
cnoremap <F3> <C-R>=strftime("%Y-%m-%d")<CR>
```

Дата будет вставляться во всех режимах - n (Normal), i (Insert) и с (Command Line).

Запишем в макрос @h быструю вставку шапки для публикации:

     " Insert header to jekyll
     let @h = "i---layout: posttitle: ---kA"` `let @h = "i---layout: posttitle: ---kA"`

Теперь при выполнении команды @h в тексте появится:

```
---
layout: post
title: 
---
```
При этом курсор расположится в поле ввода заголовка статьи title.

### Алгоритм создания публикации

1. Открыть индексную страницу нужного vimwiki командой \ww или n\ww 
2. На индексной странице предлагаю размещать список публикаций в формате "date-name-of-post". Индексная страница не публикуется, но предоставляет возможность удобной навигации по страницам.

Пример:

![alt text](/img/vw.png)

Для вставки даты нажимаем F3, затем пишем название и нажимаем Enter, после чего создается новый файл с названием в нужном формате.
3. Вставляем шапку командой @h.
4. Сохраняем.



