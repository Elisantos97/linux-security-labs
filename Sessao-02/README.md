
Análise de Logs SSH no Linux

Objetivo

O objetivo deste laboratório foi compreender como o Linux regista eventos de autenticação SSH e aprender a identificar tentativas de acesso falhadas e bem-sucedidas através da análise de logs.


Atividades Realizadas
1. Criação de utilizadores de teste

Foram criados utilizadores para simular tentativas de autenticação SSH.

useradd -m teste
useradd -m teste3
passwd teste3

2. Simulação de tentativas de login

Foram efetuadas várias tentativas de ligação SSH utilizando palavras-passe incorretas para gerar eventos de autenticação falhada.

ssh teste@localhost
ssh teste2@localhost
ssh teste3@localhost


3. Monitorização do ficheiro de logs

Foi utilizado o seguinte comando para acompanhar os eventos de autenticação em tempo real:

tail -f /var/log/auth.log


4. Identificação de autenticações falhadas

grep "Failed password" /var/log/auth.log


5. Identificação de autenticações bem-sucedidas

grep -E "Accepted password|Accepted publickey" /var/log/auth.log


6. Utilização de grep, awk, sort e uniq

grep "Failed password" /var/log/auth.log | awk '{print $11}' | sort | uniq -c | sort -nr
