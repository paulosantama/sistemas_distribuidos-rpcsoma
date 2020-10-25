NOME_PROJETO=rpcsoma

FLAGS_CLIENT=-lnsl
FLAGS_SERVER=-lrpcsvc \
			-lnsl

EXEC_CLIENT=client
EXEC_SERVER=server

build: saudacoes generateRPC pipelineCSource

saudacoes:
	@echo "Compilando $(NOME_PROJETO)"

generateRPC: simp.x
	@rpcgen -C $^

pipelineCSource: compileAllC createExecClient createExecServer

compileAllC:
	@gcc -c *.c

createExecClient: simpclient.o simp_clnt.o simp_xdr.o
	@echo "Gerando executável do client"
	@gcc -o $(EXEC_CLIENT) $^ $(FLAGS_CLIENT)

createExecServer: simpservice.o simp_svc.o simp_xdr.o
	@echo "Gerando executável do server"
	@gcc -o $(EXEC_SERVER) $^ $(FLAGS_SERVER)

clean:
	@echo "Limpando"
	@rm -f simp.h simp_* *.o $(EXEC_CLIENT) $(EXEC_SERVER)