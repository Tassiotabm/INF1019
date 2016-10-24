#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>
#include <signal.h>
#include <sys/shm.h>
#include <sys/ipc.h>
#include <sys/wait.h>
#define MAX 100

int saida = 0;

struct processo{
	char procName[10];
	int procStatus,procPid,inicio,duracao;
};
typedef struct processo Processo;

void handler(int sig)
{
     pid_t pid;
  	 pid = wait(NULL);
 	 printf("Pid %d exited.\n", pid);
}	
	
int main(int argc,char*argv[]){
	
	int fdin,fdout,retDup1,retDup2,i,idFork,procSize;
	int segmento,*memsegmento;
	int pid;
	int * regPid;
	
	//char teste[MAX_DADOS];
	
	Processo * proc,procTemp;
	proc = (Processo*)malloc(MAX*(sizeof(Processo)));
	
	//Iniciar o handler
	//signal(SIGCHLD, handler);		   
		   
	//A Pedido do prof, devemos mudar a saida dos programa para um .txt, com finalidade de melhor
	//visualizacao do programa.
	
	if((fdin=open("entradatime.txt",O_RDONLY,0666)) ==-1)
	{
		printf("Error no open entrada");
		return -1;
	}
	if((fdout=open("saida.txt",O_WRONLY|O_CREAT|O_TRUNC,0666)) ==-1){
		printf("Error no open saida");
		return -1;
	}
	
	/* Redirecionar a entrada e saída padrão para os arquivos entrada.txt e saida.txt*/
	if(retDup1 = dup2(fdin,0) == -1)
	{
		printf("Erro no dup1");
		return -2;
	}
	if(retDup2 = dup2(fdout,1) == -1)
	{
		printf("Erro no dup2");
		return -3;
	}
	
	/* Ler o entrada.txt e preencher a struct de processos */
	while(scanf("exec %s %d %d[^\n]", &proc[i].procName,&proc[i].inicio,&proc[i].duracao) != EOF)
	{
		//printf("%s\n",proc[i].procName);
		proc[i].procStatus = 0;
	    i++;
	}

	procSize = i;
	
	// "Alocar" a memoria compartilhada a ser usada
	segmento = shmget(IPC_PRIVATE, sizeof(int)*MAX,IPC_CREAT | IPC_EXCL | S_IRUSR | S_IWUSR);
	// associar a memoria compartilhada a um endereço
	// o regPid é um vetor em memoria compartilhada que guarda os PIDS dos processos
	regPid = (int*) shmat(segmento,0,0);
	
	
	
	int tempSize = 0;
	i = 0;
	while(saida<1){

		if(i==3)
			break;
		pid = fork();
		if(pid < 0){
			printf("Erro fork() \n");
			exit(1);
		}
		else if(pid == 0)
		{
			sleep(1);
			printf("Executando o processo %s",proc[i].procName);
			execve(proc[i].procName,0,0);
			exit(0);//enviar o sinal SIGCHLD finalizando o fim do processo
		}
		else if(pid > 0)
		{
			kill(pid,SIGSTOP);
			proc[i].procPid = pid;
			regPid[i] = pid;
			
			sleep(proc[i].inicio);	// Esperar ate o inicio do processo
			kill(pid,SIGCONT);	// Continuar o processo
			
			waitpid(-1,0,0); //Esperar o processo terminar
			
			
			printf("Vamos finalizar:\n Processo: %s PID: %d\n",proc[i].procName,proc[i].procPid);
			i++;
		}
	}
	
	

	return 0;	
}
