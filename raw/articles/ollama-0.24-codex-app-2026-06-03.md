---
source_url: https://mail.google.com/mail/u/0/#inbox/FMfcgzQgLrssQWjKxfvXznmcsbkLsBSJ
ingested: 2026-06-03
sha256: ac6ec124cf983d7af03c12e8d089486324a3ed7b09851ea17c43099bdb745ff5
---
## Ollama 0.24 is now available with support for OpenAI’s Codex App (Ollama 0.24 теперь доступна с поддержкой приложения Codex от OpenAI.)

|   |
|---|
|Ollama 0.24 теперь доступна с поддержкой приложения Codex App, настольной версии OpenAI для параллельной работы над потоками Codex со встроенной поддержкой дерева задач и функциональностью Git.|
||
|\|   \|<br>\|---\|<br>\|![](https://ci3.googleusercontent.com/meips/ADKq_NbfhjIrNmGT65V_e5GFEK_kjJrrV2eeCYuMluKwJBp1n2vX-kfUqKWggivceCpoIh0Xjeb0_iYvcHxi9d-qKTiJQmTpid9Cpzgabs3Wy03rstakpJ3vRkzZ6HjPjDHikRP5f_f7X_WULg=s0-d-e1-ft#https://images.vialoops.com/cmp60u9ix0a4i0j15th3zyig1/cmp61deyt2e0m0jzud7nhm2r3.png)\||
||
|### Начните|
|[Скачайте Ollama 0.24](https://c.vialoops.com/CL0/https:%2F%2Follama.com%2Fdownload/1/0100019e2a6dbb61-8e31a9cd-ea0e-4abc-81b5-e5d74a0c0120-000000/-9eV3RVJ6af86M7CnNwDsNv3RJdHbcx-22elGUajYK8=452) , затем запустите:|
||
|`ollama launch codex-app`|
||
|### Встроенный браузер|
|Codex может загружать локальные серверы и сайты в свой встроенный браузер, что позволяет напрямую добавлять аннотации на страницу для запроса изменений.|
||
|\|   \|<br>\|---\|<br>\|![](https://ci3.googleusercontent.com/meips/ADKq_NYMBGAHOcni2e2W0iE48ssqWrHUIsO-6Rbo9UKoRKGcU8AXBIWCaguioHwniKrRp2HErrUFa1QUuyKtm1xdxGFSIVdX-JMdhc7MMPgkUds6Q3zNfOge3QyEOpqvR1HlVw_fL7BjhVP18A=s0-d-e1-ft#https://images.vialoops.com/cmp60u9ix0a4i0j15th3zyig1/cmp61522j00e70izvfnxuo8zz.png)\||
||
|### Режим обзора|
|Просматривайте код прямо в приложении, оставляйте комментарии и вносите изменения, не покидая рабочее пространство.|
||
|\|   \|<br>\|---\|<br>\|![](https://ci3.googleusercontent.com/meips/ADKq_NYiSNjK7168suE3uHMm5OqqbDLa5GsVBjFl3k4OJwKhCSvAdj2Yh0je3uwff0S6OmlfTzNp2Zf9-mX6htX0Bb5gDdAfP2YmACUCI0RNnWbJ-rmHMeLw1TgCHbodKS55YHRYuzXR4i1G2g=s0-d-e1-ft#https://images.vialoops.com/cmp60u9ix0a4i0j15th3zyig1/cmp62opuf1py80j26p3mrjiy9.png)\||
||
|### Выбор модели|
|Для задач программирования и работы с агентами:|
|- kimi-k2.6:cloud (с поддержкой машинного зрения)|
|- glm-5.1:cloud|
||
|Если у вас еще нет платной подписки на облачные сервисы Ollama, выберите модель, поддерживающую надежный вызов инструментов:|
|- nemotron-3-super:cloud|
|- gemma4:31b:cloud|
|- qwen3.6|
||
|### Восстановление моделей по умолчанию|
|Для восстановления профиля Codex по умолчанию используйте параметр --restore :|
||
|`ollama launch codex-app --restore`|
||