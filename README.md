

1. Найдите полный хеш и комментарий коммита, хеш которого начинается на aefea. Полный хэш: aefead2207ef7e2aa5dc81a34aedf0cad4c32545 Комментарий коммита: Update CHANGELOG.md

_Узнал по команде git show aefea

2. Какому тегу соответствует коммит 85024d3? v0.12.23

_Узнал по команде git show 85024d3

3. Сколько родителей у коммита b8d720? Напишите их хеши. Коммит b8d720 (полный хэш: 56cd7859e05c36c06b56d013b55a252d0bb7e158) является мерж-коммитом,у него 2 родителя: 58dcac4b7 (Полный хэш: 58dcac4b798f0a2421170d84e507a42838101648) (tag: v0.12.19) ffbcf5581 (Полный хэш: ffbcf55817cb96f6d5ffe1a34abe963b159bf34e)

_Узнал по команде git show b8d720^

4. Перечислите хеши и комментарии всех коммитов которые были сделаны между тегами v0.12.23 и v0.12.24.

33ff1c03b (tag: v0.12.24) v0.12.24 b14b74c49 [Website] vmc provider links 3f235065b Update CHANGELOG.md 6ae64e247 registry: Fix panic when server is unreachable 5c619ca1b website: Remove links to the getting started guide's old location 06275647e Update CHANGELOG.md d5f9411f5 command: Fix bug when using terraform login on Windows 4b6d06cc5 Update CHANGELOG.md dd01a3507 Update CHANGELOG.md 225466bc3 (HEAD) Cleanup after v0.12.23 release 85024d310 (tag: v0.12.23) v0.12.23

_Посмотрел командой git log v0.12.23~...v0.12.24 --oneline

5. Найдите коммит в котором была создана функция func providerSource, ее определение в коде выглядит так func providerSource(...) (вместо троеточего перечислены аргументы).

Коммит, в котором функция была создана: 18dd1bb4d6134b9f8e15b9cea7fae0c878d0a8ba

_Сначала нашел файл, где данная функция описана: git grep --break --heading -n -e 'providerSource' _Затем нашел по данному файлу коммит создания: git log -L :TestInit_providerSource:command/init_test.go

6. Найдите все коммиты в которых была изменена функция globalPluginDirs 78b12205587fe839f10d946ea3fdc06719decb05 52dbf94834cb970b510f2fba853a5b49ad9b1a46 41ab0aef7a0fe030e84018973a64135b11abcd70 66ebff90cdfaa6938f26f908c7ebad8d547fea17 8364383c359a6b738a436d1b7745ccdce178df47

_Сначала нашел файл, где данная функция описана: git grep --break --heading -n -e 'globalPluginDirs' _Затем нашел по данному файлу все коммиты, где функция была изменена: git log -L :TestInit_providerSource:command/init_test.go

7. Кто автор функции synchronizedWriters? Автор функции: : Martin Atkins mart@degeneration.co.uk, добавлена в коммите 5ac311e2a91e381e2f52234668b49ba670aa0fe5 3.05.2017

_Сначала нашел файл, где данная функция описана: git grep --break --heading -n -e 'synchronizedWriters' _Затем нашел по данному файлу все коммиты, это был 1 коммит, посмотрел автора коммита: git log -L :synchronizedWriters:synchronized_writers.go
