OFX-BOT
=============

Estes bots tem por objetivo automatizar a tarefa de conciliação bancária entre contas do Banco do Brasil,
Caixa Econômica, Itaú, Santander e NuBank com aplicativos que aceitam o formato 'ofx' (GNUCash, HomeBank.free.fr, Microsoft Money). 

#### ofx-bb:
* Baixa o 'ofx' da conta corrente
* Baixa o 'ofx' da poupança
* Baixa o 'ofx' do cartão de crédito 'Petrobrás'

#### ofx-caixa:
* Baixa o 'ofx' da conta corrente

#### ofx-itau:
* Baixa o 'ofx' da conta corrente

#### ofx-santander:
* Baixa o 'ofx' da conta corrente

#### ofx-nubank:
* Baixa o 'ofx' dos lançamentos das faturas disponíveis. Também é capaz de gerar
um CSV no formato aceito pelo HomeBank (Veja: ofx-nubank --help)


Requisitos:
--------------

#### ofx-bb, ofx-caixa e ofx-santander
* É necessário ter o pacote **selenium** do Python2:

```bash
pip2 install selenium
```

#### ofx-itau, ofx-nubank

* É necessário ter o Haskell Stack instalado:

```bash
wget -q -O- https://s3.amazonaws.com/download.fpcomplete.com/ubuntu/fpco.key | sudo apt-key add -
echo "deb http://download.fpcomplete.com/ubuntu/$(lsb_release -sc) stable main"|sudo tee /etc/apt/sources.list.d/fpco.list
sudo apt-get update
sudo apt-get install stack
```

* Para compilar:

```bash
cd itau
./build.sh
```
ou 

```bash
cd nubank
./build.sh
```

* Caso a sua instalação de Haskell seja nova, o ``build.sh`` baixará e instalará uma série de pacotes no ``~/.stack``. Isso pode levar algum tempo. 
Após compilado, os executáveis são automaticamente copiados para o diretório raiz do projeto.


Como usar:
-------------

```bash
./ofx-bb.py
./ofx-caixa.py
./ofx-itau
./ofx-santander.py
./ofx-nubank
```
Ou usando um aquivo de entrada, via redirecionamento:

```bash
./ofx-bb.py < input.cfg
./ofx-caixa.py < input.cfg
./ofx-itau < input.cfg
./ofx-santander.py < input.cfg
./ofx-nubank < input.cfg
```

Nos casos acima, a janela do Firefox ficará visível durante toda a execução dos bots, pois não há 
nenhum tratamento com o display. Este comportamento é interessante para acompanhar o movimento 
nas páginas e depurar possíveis bugs. Para deixar o browser oculto, utilize um display virtual,
como no exemplo abaixo:

```bash
xvfb-run --server-args="-screen 0, 1440x900x24" ./ofx-bb.py < input.cfg
```

Notas:
------------

Obviamente, este script supre minhas necessidades. Porém ele pode se tornar bem mais elaborado.
Alguns pontos a se melhorar futuramente:

* Criptografar a senha com a chave privada do usuário para evitar a digitação em todas execuções
* Opção de mais 'ofx' de acordo com o desejo do usuário (Poupança, outros cartões, ...)
* Mais tarefas automatizadas 

