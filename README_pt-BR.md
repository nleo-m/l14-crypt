# l14-crypt
Codificador/decodificador de mensagens com alguns métodos de cifra de transposição.

## Cifras disponíveis

### Reverso or r
Como o nome já sugere, retorna a mensagem invertida;

eg: Hello world = dlrowolleH

### César or c
Esta cifra foi usada pelo imperador romano Júlio César, daí o nome. É um tipo de cifra de substituição na qual cada letra é substituída por outra em um intervalo definido, usado com --shift ou -s para defini-lo. [Mais informações](https://en.wikipedia.org/wiki/Caesar_cipher);

eg: Hello world = Khoorzruog
Deslocação (shift) padrão usada, que é 3.

### Caractere para número or n
Substitui cada letra pelo o número que corresponde a sua posição no alfabeto.

eg: Hello world = 8 5 12 12 15 23 15 18 12 4
A = 1, B = 2, C = 3 ... 

### Matriz horizontal or h
Também chamado de [Transposição colunar](https://pt.wikipedia.org/wiki/Cifra_de_transposição#Transposição_de_colunas). Use --horizontal_shift or -hs para definir o tamanho da coluna;

eg: Hello world = Holewdlolr
Tamanho padrão de coluna usada (horizontal_shift), que é 4.

### Alternado primeiro para o segundo or a
Substitua o primeiro pelo segundo, o terceiro pelo quarto e assim por diante; 

eg: Hello world = eHllo owlrd

### Chave de transposição aleatória or rk
Reorganiza a mensagem aleatoriamente, e gera uma chave com os índices de posição original para decriptação;  

eg: Hello world = dlHwrlleo o
Generated key: 10 9 0 6 8 2 3 1 7 5 4


## Possíveis argumentos

### --help or -h
Sem surpresas, exibe mensagem de ajuda e uso;

### --shift or -s
Use com o método de Caesar para definir a deslocação, o padrão é três;

### --horizontal_shift or -hs
O mesmo que shift, mas para definir o tamanho da coluna da matriz horizontal, o padrão é quatro;

### --preserve_whitespaces or -pw
Use-o para preservar espaços em branco. Tenha em mente que isso pode alterar o resultado com alguns métodos, sendo necessário passar como argumento ao decriptar, o padrão é false;

### --key or -k
Especifica a chave para descriptografar mensagens na descriptografia baseada em chave;

### --output or -o
Salva em um arquivo externo. O primeiro argumento é para localização, o outro para o método (w)rite ou (a)ppend;

### --input or -i
Abre um arquivo externo e usa como mensagem, basta digitar a localização do arquivo;

### --clear or -c
Tenta limpar a tela antes de mostrar a mensagem cifrada, o padrão é false;

### --copy or -co
Tenta copiar a mensagem cifrada para a área de transferência usando clip em sistemas windows, pbcopy no mac, e xsel para área de transferência ou xclip em sistemas linux. O padrão é false;

## Exemplos de uso

python3 main.py "just testing" e a r  
Output: ginsttestju
A mensagem é "just testing", Eu quero (e)ncriptar usando os métodos (a)lternato e (r)everso;

./main.py "ginsttestju" d reverse alternate  
Output: justtesting
Estou em um sistema unix como e dei permissões de execução ao meu script main.py, passei a saída anterior como mensagem de entrada para (d)ecriptação usando os métodos (r)everso e (a)lternado. Você entendeu a ideia, certo? Como criptografei usando alternado e depois reverso, primeiro preciso reverter e depois alternar para chegar à mensagem original. Os espaços em branco não foram preservados, portanto, as palavras ficam grudadas.

./main.py "Hello World" e c -s 10 -pw  
Output: Rovvy Gybvn

./main.py "Hello World" e h --horizontal_shift 2 -pw --copy  
Output: HloWrdel ol  
Sucessfully copied to clipboard

./main.py "lHoold rWle" d ra -k 9 0 4 7 3 10 5 8 6 2 1 --preserve_whitespaces -o ./my_output.txt w  
Output: Hello World 

./main.py --input ./my_output.txt e reverse  
Output: dlroWolleH 