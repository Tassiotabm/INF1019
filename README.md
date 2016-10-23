# INF1019
Trabalho I

Primeiro'Trabalho'de'Sistemas'de'Computação'– INF'1019
O"primeiro"trabalho"consiste"em"programar"em"linguagem"C"programas"que"implementem um"
interpretador"de"comandos"e"um"escalonador de"programas."O"interpretador"deverá"solicitar"
ao"escalonador"a"execução de" programas."O"escalonador" por" sua" vez" dispara"a"execução"de
programas"de"acordo"com"uma"determinada"política"de"escalonamento,"que"deverá ser:
PRIORIDADE" (neste"caso"o"interpretador"deve"indicar"ao"escalonador"uma"prioridade"
de"execução""que"é"um"número"de"1"a"7"sendo"1"a"maior"prioridade"e"7"a"menor)".
ROUNDNROBIN"(com"timeNsharing"e"fatia"de"tempo"de"0.5"segundos)
1
REALNTIME (nesse"caso"o"interpretador"deve"indicar"ao"escalonador"em"qual"segundo"e"
por"quantos"segundos"o"processo"deverá"executar)
Na política" de" escalonamento" REALNTIME" cada" processo" deverá" iniciar" sua" execução,
periodicamente (uma" vez" por minuto), em" determinado" momento" e" deve" permanecer"
executando"apenas"durante"um"certo"período"de"tempo."Tanto"o"momento"de"início"como"a"
duração"são"indicados"pelos"seus"parâmetros."Por"exemplo,"P1"I=20"D=5,"indica"que"P1"deve"
ser"executado"a"cada"minuto"e"20"segundos"e"deve"executar"por"5"segundos,"ou"seja,"do M:20"
até" o" M:25" (onde" M" significa" cada" minuto)." Para" esse" tipo" de" escalonamento" o" seu"
escalonador" deverá" verificar" se" um" novo" processo" iniciado" não" possui" parâmetros" de"
escalonamento"conflitantes"com"os"dos"demais"processos"já em"execução."Por"exemplo,"se"seu"
escalonado"já"está executando"P1"I=0"D=10"e"P2"I=20"D=5,"então"não" será"possível"executar"
um"processo"P3"I=11"D=20,"pois"não"haveria"como"permitir"a"execução"simultânea"de"P2"e"P3."
Voce"também"deverá"verificar"se"I+D"<="60"segundos.
O"Unix tem"um"escalonador"próprio"mas"o"escalonador"do" trabalho"é"quem"vai"coordenar"a"
execução" dos" processos" indicados" pelo" usuário" no" interpretador" de" comandos." Ou" seja," o"
escalonador" é" quem" vai controlar a" ordem" de" execução" dos" programas realizando" a
preempção, através" de" alguma" forma" de comunicação" entre" processos" (vai" indicar" a"
interrupção"da"execução"de"um"processo"e"a"continuidade da"sua"execução).
Além"disso,"o"seu"Interpretador"deverá usar algum"tipo"de"comunicação"interNprocesso"(shared"
memory,"pipes,"Named"pipes"ou"Message"Queues)"para"passar"os"dados"dos"programas"para"o"
Escalonador:
Interpretador" de" comandos" " N>" Escalonador" N>" chamadas" ao" Sistema" Operacional"
(fork/exec,"kill,"signal,"etc.)"
O"Escalonador"deve"ter"estruturas"de"dados"capazes"de"possibilitar a"execução"destas"políticas."
Você pode" implementar" três escalonadores" próprios," cada" um" implementando" uma" das"
políticas acima.""Ou"então,"caso"você"queira implementar"um"único"escalonador"para"todas"as"
politicas"então"considere"a"seguinte"hierarquia"de"prioridades"entre"as"3"politicas:
REALNTIME">>"Prioridade"1">>"Prioridade"7"">>""ROUNDNROBIN"
"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""" 1 Esse"valor"da"fatia"de"tempo"pode"ser"redefinido,"caso"os"resultado"do"escalonamento"não"se"mostre"expressivo.
A"linguagem"a"ser"analisada"pelo interpretador"de"comandos"é"a"seguinte (cada"comando"em"
uma"linha):
Exec"<nome_programa>"PR=<numero"de"1"a"7>,"para" escescalonamento""prioridades
Exec <nome_programa>,"para"o"ROUNDNROBIN
Exec"<nome_programa>"I=<segundoNinício>"D=<tempoNduração>,"para" REALNTIME
Os"programas"(“nome_programa”)"a"serem"escalonados/executados"devem ser"de"dois"tipos:"
CPUNbound"e"IONbound e"devem"ser"criados"por"voces."A"entrada"padrão"e"a"saída"padrão"dos"
processos"devem ser"redirecionadas"para"os"arquivos"entrada.txt"e"saída.txt,"respectivamente."
O interpretador"irá"ler"de"exec.txt"quais"são"os"programas"a"serem"executados,"e"deverá"iniciaN
los"exatamente"na"ordem"em"que"aparecem nesse"arquivo,"com"uma"diferença"de"1 segundos"
entre"cada"um"deles. A"saída"deve"ser"clara"o"suficiente"para"mostrar"como"e"porque"ocorre"a"
preempção"na"execução"dos"processos. Esses"arquivos"serão"objetos"de"avaliação.
O"trabalho"pode"ser"feito"de"forma"individual"ou"em"dupla."O"trabalho"será avaliado em"28/04
na" aula" de" laboratório," logo," deve" ser" enviado até" 19/10 às" 23:59:59”" via" eNmail" para:
jessicatsalmeida@gmail.com, e endler@inf.pucNrio.br
Deve"ser"entregue"o"código" fonte"e"um" relatório"indicando"que"programas"serão"executados"
em" seu" teste," a" ordem" de"entrada" para" o"escalonador"e" a" ordem" de"execução" determinada"
pelo" escalonador," juntamente" com" uma" análise" crítica" sobre" o" que," de" fato," ocorreu. Essa"
explicação"também"será"objeto"de"avaliação.
