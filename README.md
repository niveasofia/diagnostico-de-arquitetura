## Diário de Bordo: Encontro 8

**Disciplina:** Sistemas Operacionais<br>
**Tema:** Diagnóstico de Arquitetura - O Gargalo da Memória Virtual<br>
**Alunos:** Nivea Sofia da Cas || Roberto Müller

## Parte A: O Fenômeno da Paginação e o Gargalo do Disco

## Parte B: O Papel e a Eficiência da TLB

### 1. O que é a TLB (Translation Lookaside Buffer) e por que ela é implementada em hardware (na MMU) em vez de ser uma tabela comum na memória RAM?

É um pequeno dispositivo de hardware que mapeia os endereços virtuais para endereços físicos sem precisar passar pela tabela de páginas.

Porque, se ela estivesse na memória RAM, seriam necessários dois pontos de referência, ou seja, dois acessos à memória: um para acessar a tabela de páginas e outro para acessar o dado propriamente.

Assim, na MMU, ela confere se o número da página virtual está na TLB, comparando todas as entradas simultaneamente. A tabela de páginas só vai ser acessada se o número da página não estiver na TLB.


### 2. Explique como uma alta taxa de "TLB miss" (erros na TLB) afeta o tempo de resposta do servidor. O que acontece com o conteúdo da TLB a cada vez que o Sistema Operacional realiza uma troca de contexto entre os processos do banco de dados?

Depende se é **soft miss** ou **hard miss**.

- **Soft miss:** ocorre quando a página referenciada não se encontra na TLB, mas está na memória. Só é necessário atualizar a TLB, em torno de 10 a 20 instruções, que levam nanossegundos. Embora mais leve, ainda exige acessos extras à memória.
- **Hard miss:** ocorre quando a página não está na memória e nem na TLB. É necessário acessar o disco, o que pode demorar vários milissegundos, dependendo do disco usado. Uma hard miss é bem mais demorada do que uma soft miss.

Em caso de uma alta taxa de misses, o tempo médio de acesso à memória aumenta e as respostas ficam mais lentas.

**Troca de contexto:** a cada troca de contexto, a TLB precisa ser descarregada para se livrar de traços do processo que estava sendo executado, pois as entradas guardam mapeamentos do processo anterior, e uma mesma página virtual aponta para quadros diferentes em cada processo. Então a tabela de páginas do novo processo, se torna a atual.

O novo processo gera uma sequência de misses até reconstruir o conjunto de páginas ativas. Em um banco de dados, com muitos processos se alternando, isso custa desempenho.

## Parte C: Síntese e Solução

## Mapa Mental

<div align="center">
    <img src="mapa.jpg" alt="mapa mental" width="500">
    <br>Fonte: elaborado pelos autores (2026).
</div>


## Referências

### Texto

TANENBAUM, Andrew S.; BOS, Herbert. **Sistemas operacionais modernos**. Tradução: Jorge Ritter. Revisão técnica: Raphael Y. de Camargo. 4. ed. São Paulo: Pearson Education do Brasil, 2016.

### Vídeo

DICIONÁRIO DE INFORMÁTICA. Memória VIRTUAL. [S. l.]: YouTube, 11 set. 2020. 1 vídeo (9 min 34 s). Disponível em: https://www.youtube.com/watch?v=z11N1DhgYO0.