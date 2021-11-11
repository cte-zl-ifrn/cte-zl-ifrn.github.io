# Ecossistema do CTE/ZL/IFRN

A Coordenação de Tecnologias da Educação (CTE) do [Campus Avançado Nata-Zona Leste (ZL)](https://ead.ifrn.edu.br/portal/) do [Instituto Federal de Educação, Ciência e Tecnologia do Rio Grande do Norte (IFRN)](https://ifrn.edu.br/) utiliza um ecossistema de aplicações para suportar o Ambiente Virtual de Aprendizagem (AVA). Neste site existe uma visão de como este ecossistema foi arquitetado para que você possa tentar se inspirar e reproduzir em seu ambiente a fim de melhorar a oferta de serviço AVA a sua comunidade acadêmica.

Se você quiser ver o desenho arquitetural da solução ela está documentada usando o [C4 Model](c4_model). Agora, se você tem tempo, segue a documentação rápida do que fazer (aqui não teremos os manuais de instalação do Moodle, do Plugin auth_suap ou do SUAP).

## No Moodle

Edite o `local_settings.py` de tua instalação e defina a configuração `MOODLE_SYNC_TOKEN` com o valor e `MOODLE_SYNC_URL`.

## No PORTAL_AVA

Depois de colocar o [PORTAL_AVA](https://github.com/cte-zl-ifrn/portal__ava) para executar conforme o README do software, configure ao menos a variável de ambiente `SUAP_EAD_KEY` em `confs/enabled/avaportal.env`. Outras configurações serão necessárias, esta é necessária para a autenticação do SUAP neste serviço. Também será necessário configura a URL e o token de autenticação de cada Moodle de cada campus.

## No SUAP

Edite o `local_settings.py` de tua instalação e defina as configurações:

* `MOODLE_SYNC_URL` com a URL raiz do AVA_PORTAL (ex.: "https://ava.if.edu.br/").
* `MOODLE_SYNC_TOKEN` com o valor que foi o que você especificou no **PORTAL_AVA**, arquivo `confs/enabled/avaportal.env`, variável de ambiente `SUAP_EAD_KEY`.
