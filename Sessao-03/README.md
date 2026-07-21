Sessão 03 — Hardening de Redes Linux e Configuração de Firewalls

Objetivo

O objetivo deste laboratório foi aplicar uma política defensiva num
sistema Linux utilizando o UFW e o iptables, bloqueando ligações de
entrada não autorizadas e permitindo apenas o acesso SSH pela porta 22.

Ambiente

-   Plataforma: KillerCoda Ubuntu Playground
-   Sistema Operativo: Ubuntu 24.04
-   Ferramentas utilizadas:
    -   UFW
    -   iptables
    -   iptables-save

Atividades Realizadas

1. Verificação do estado do UFW

Comando:

    sudo ufw status

Resultado observado:

    Status: inactive

Verificou-se que o UFW estava instalado, mas ainda não se encontrava
ativo.

Para ativar foi utilizado o comando:

    sudo ufw enable


2. Configuração das políticas padrão

Foram aplicadas as seguintes políticas:

    sudo ufw default deny incoming
    sudo ufw default allow outgoing

Estas regras bloqueiam todas as ligações de entrada por defeito e
permitem o tráfego de saída.

3. Permissão do acesso SSH

Foi criada uma regra para permitir apenas ligações SSH na porta TCP 22.

    sudo ufw allow 22/tcp

4. Simulação de bloqueio de um IP malicioso

Foi adicionada uma regra ao iptables para bloquear o endereço IP
fictício:

    203.0.113.50

Comando utilizado:

    sudo iptables -A INPUT -s 203.0.113.50 -j DROP

5. Verificação das regras

Foram utilizados os comandos:

    sudo ufw status verbose
    sudo iptables -L -v

A regra criada apareceu na chain INPUT, indicando que qualquer tráfego
proveniente do IP 203.0.113.50 seria descartado.

6. Persistência das regras

Foi tentado guardar o estado do iptables utilizando:

    sudo iptables-save | sudo tee /etc/iptables/rules.v4


Política Aplicada

A política implementada segue o princípio de “negar por defeito”.

-   Bloquear todas as ligações de entrada.
-   Permitir todas as ligações de saída.
-   Permitir apenas SSH na porta 22.
-   Bloquear o IP fictício 203.0.113.50.

Competências Desenvolvidas

-   Configuração de UFW
-   Configuração de iptables
-   Hardening de sistemas Linux
-   Gestão de regras de firewall
-   Bloqueio de endereços IP
-   Análise de regras de segurança



Conclusão

Este laboratório permitiu compreender como configurar uma firewall em
Linux utilizando UFW e iptables. Foram aplicadas regras de segurança
para restringir o acesso ao servidor, permitindo apenas o serviço SSH e
simulando o bloqueio de um endereço IP malicioso.
