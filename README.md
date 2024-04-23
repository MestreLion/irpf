Instalador do IRPF
==================

Download automático e instalação dos programas de Imposto de Renda Pessoa Física em plataformas no GNU/Linux, em particular Debian, Ubuntu e derivados.

Possui as seguintes características e vantagens sobre o instalador oficial da Receita:

- **Download automático dos programas**
  > Diretamente dos servidores da Receita, de qualquer ano desde 2008, sem necessidade de navegar e procurar no site da RF.
- **Verificação de integridade do download** através de checksums pré-computados.
  > Como o site da Receita infelizmente não informa os _hashes_ dos arquivos, não é possível o usuário final verificar se o programa foi corrompido ou alterado
    (maliciosamente ou por erro). Para contornar isso eu baixo e calculo os hashes de cada versão publicada todo ano.
    Consulte-os em [`sha256sum.txt`](./sha256sum.txt).
- **Não necessita de privilégios administrativos para instalação.**
  > Por padrão a instalação é apenas para o seu próprio usuário, sem precisar de `sudo` (caso o Java já esteja instalado na máquina).
    Todos os arquivos baixados e instalados ficam em subpastas de `~/.local`, não modificando nada do sistema.
- **Instala corretamente ícones e entradas de menu**.
  > O instalador oficial da Receita cria um grupo de menu pra _cada_ ano, além de criar ícones no desktop de _todos_
    os usuários. Este instalador gera um único grupo `Programas RFB`, utilizando o ícone oficial, e _opcionalmente_ adiciona os ícones `Ajuda` (em PDF) e `Leia-me`,
    caso solicitado, além de adicionar ícones no Desktop apenas do usuário atual, e também apenas caso socilicitado.
- **Não traz o Java inteiro embutido**, utilizando o Java já instalado no sistema e instalando a versão apropriada caso necessário.
- Instala o Receitanet e o IRPF em uma única etapa. Receitanet era necessário para os programas do IRPF até 2017.
- Não utiliza GUI, podendo ser automatizado para instalação em massa do IRPF de vários anos.


Requisitos
----------

O único requisito do programa do IRPF é o **Java**, e este instalador já automaticamente instala o OpenJDK padrão
do seu sistema caso necessário.

    sudo apt install default-jdk

Instalação
----------

Basta fazer o clone do repositório e executar `./install`, que por padrão baixa e instala o IRPF do ano atual.
Sugere-se fazer o clone em `~/.local/share/irpf`:

```sh
cd ~/.local/share
git clone https://github.com/MestreLion/irpf.git
irpf/install
```

Uso
---

```console
$ ./install --help
Uso: install [opções]

Instalador para os programas da Receita Federal (IRPF e ReceitaNet)

Inclui download dos programas, verificação de integridade, entradas de menu
com ícones oficiais, instalação e remoção sem necessidade de privilégios
administrativos (root).

Testado com todos os programas da Receita desde 2008.

Opções gerais:
  -h|--help  - Exibe esta página de ajuda.
  -q|--quiet - Não exibe mensagens informativas, como o progresso da instalação.
  -y|--yes   - Automaticamente responde SIM a todas as perguntas de confirmação.
  -f|--force - Força ações mesmo que sejam redundantes, por exemplo instalação
               de programas já existentes (sobrescrevendo arquivos) ou a remoção
               de programas inexistentes.

Opções de pasta:
  --rootdir PATH
	Raiz comum da pasta de instalação dos programas.
	Cada programa, IRPF de cada ano ou ReceitaNet, será instalado em uma
	subpasta desta raiz.  O padrão é '/home/rodrigo/.local/opt/ProgramasRFB'

  --download PATH
	Pasta para download dos programas.
	O padrão é '/home/rodrigo/.local/opt/ProgramasRFB/download'

Opções de instalação:
  --irpf ANO
	Instala o IRPF de um ano específico.

  --receitanet
	Instala (ou atualiza) a versão mais atual do ReceitaNet.

Se nenhuma das opções de instalação acima forem selecionadas, por padrão instala
o IRPF do ano atual, 2024. O programa ReceitaNet não é mais necessário a partir
do IRPF 2017.

  --no-java
	Não verifica a versão do Java nem tenta instalá-lo caso ausente.
	O IRPF exige Java instalado no sistema, e de 2021 em diante recomenda
	uma versão específica. Por padrão a instalação verifica e instala o
	Java apropriado, o que requer privilégios administrativos (root/sudo).

Opções de menus:
  --menu-ajuda
	Cria a entrada de menu para a 'Ajuda', um documento em formato PDF.
	O mesmo conteúdo desta Ajuda também está disponível em outro formato,
	a partir do próprio programa do IRPF, selecionando Ajuda -> Conteúdo,
	portanto esta entrada de menu é redundante.

  --menu-leiame
	Cria a entrada de menu para o 'Leia-me'. Contém apenas instruções da
	Receita para instalação do IRPF e da máquina virtual Java, com ênfase no
	ambiente Windows, sendo portanto desnecessária em ambiente GNU/Linux.

  --desktop
	Além das entradas de menu, cria também ícones na área de trabalho.

Opções de remoção:
  --uninstall
	Remove o ReceitaNet ou o IRPF de um ano específico.
	Deve ser utilizada em conjunto com --receitanet ou --irpf ANO.

  --uninstall-all
	Remove todos os programas da Receita.
	Não deve ser utilizado com nenhuma outra opção além de --rootdir.
	Por segurança, o uso em conjunto com --irpf, --receitanet ou --uninstall
	resulta em erro. Demais opções são ignoradas.
```

Exemplo:
```console
$ ./install 
* Opções selecionadas:
- Programa do IRPF:   2024
- Receitanet:         Não
- Ícones no Desktop:  Não
- Inclui menu Ajuda:  Não
- Inclui menu Leiame: Não
- Pasta downloads:    /home/rodrigo/.local/opt/ProgramasRFB/download
- Pasta principal:    /home/rodrigo/.local/opt/ProgramasRFB

Confirma? (s/n, padrão NÃO): s

* Baixando o IRPF 2024: IRPF2024-1.1.zip
--2024-04-23 16:00:16--  https://downloadirpf.receita.fazenda.gov.br/irpf/2024/irpf/arquivos/IRPF2024-1.1.zip
Resolving downloadirpf.receita.fazenda.gov.br (downloadirpf.receita.fazenda.gov.br)... 161.148.231.16
Connecting to downloadirpf.receita.fazenda.gov.br (downloadirpf.receita.fazenda.gov.br)|161.148.231.16|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 50379578 (48M) [application/zip]
Saving to: ‘/home/rodrigo/.local/opt/ProgramasRFB/download/IRPF2024-1.1.zip’

IRPF2024-1.1.zip  100%[======================================================================>]  48.04M  2.92MB/s  in 17s

2024-04-23 16:00:33 (2.87 MB/s) - ‘/home/rodrigo/.local/opt/ProgramasRFB/download/IRPF2024-1.1.zip’ saved [50379578/50379578]

* Verificando integridade do arquivo
/home/rodrigo/.local/opt/ProgramasRFB/download/IRPF2024-1.1.zip: OK
* Instalando o IRPF 2024
* Gerando script de remoção para o IRPF 2024
* Pronto!
```

Estrutura:
```
$ ls -l ~/.local/opt/ProgramasRFB/
total 45,056
drwxrwxr-x 2 rodrigo rodrigo  4,096 2024-04-23 16:07 download
drwxrwxr-x 5 rodrigo rodrigo  4,096 2022-04-28 22:32 IRPF2022
drwxrwxr-x 6 rodrigo rodrigo  4,096 2023-05-25 23:15 IRPF2023
drwxrwxr-x 6 rodrigo rodrigo  4,096 2024-04-23 16:00 IRPF2024
drwxrwxr-x 2 rodrigo rodrigo  4,096 2024-04-23 16:00 xdg
-rwxrwxr-x 1 rodrigo rodrigo 23,311 2022-05-01 22:52 uninstall
```

Desinstalação
-------------

Basta usar a opção `--uninstall-all` para remover todos os programas e então apagar o repositório local:
```sh
~/.local/share/irpf/install --uninstall-all
rm -rf ~/.local/share/irpf
```

Ou, caso não tenha mais o repositório git local, use o `uninstall` que foi gerado na pasta de instalação:
```sh
~/.local/opt/ProgramasRFB/uninstall
```
---

Autor
-----

Rodrigo Silva (MestreLion) <linux@rodrigosilva.com>

Licença e Copyright
-------------------
```
Copyright (C) 2015 Rodrigo Silva (MestreLion) <linux@rodrigosilva.com>.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
```
