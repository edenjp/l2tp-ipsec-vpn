# l2tp-ipsec-vpn

 l2tp-ipsec-vpn for ubuntu 14.04

## Instalando os pacotes


### Pacotes requeridos:

$ sudo `apt-get install openswan`

$ sudo `apt-get install xl2tpd`

$ sudo `apt-get install l2tp-ipsec-vpn`

conclua com `reboot` da máquina 

Caso não seja possível encontrar os pacotes, faça clone dos arquivos disponível neste github. 


>  Configurando o  l2tp-ipsec-vpn

`Passo 1` - Baixe os arquivos deste diretório.

$ git clone [url]

Após isto, instale os arquivos do diretório:

$ sudo dpkg -i openswan*.deb 

$ sudo dpkg -i *.deb


`Passo 2` - Execute o **L2TP Ipsec VPN Applet**


`Passo 3` - No novo ícone disponível, clique em **Edit Connections**


`Passo 4` - Clique em **Add**


`Passo 5` - Preencha com nome da "SuaVPN" e clique em OK


`Passo 6` - Selecione "SuaVPN" e clique em **Edit**


`Passo 7` - Na aba IPsec preencha os campos, use a pre-shared key do seu servidor  XXXXXXXXXXXXXXXXXXXXXXXX


`Passo 8` - Na aba **L2TP** habilite o **Length Bit**


`Passo 9` - Na aba PPP  máquina **Allow these protocols** e preencha os campos de **user name** e **password**


`Passo 10` - Clique em **IP Settings** e habilite **Obtain DNS server address automatically** , depois  finalize as configurações


`Passo 11` - Para conectar basta clicar na sua  SuaVPN ( * *pode demorar por volta de 30 segundos* ) 

### Caso ainda tenha alguma dificuldade configure sua VPN conforme o exemplo 


$ `sudo vim /etc/ppp/<Sua_VPN>.options.xl2tpd`

```
# /etc/ppp/SuaVPN.options.xl2tpd - Options used by PPP when a connection is made by an L2TP daemon
# $Id$

# Manual: PPPD(8)

# Created: sáb mai 30 22:57:50 2015
#      by: The L2TP IPsec VPN Manager application version 1.0.9
#
# WARNING! All changes made in this file will be lost!

#debug
#dump
#record /var/log/pppd

plugin passprompt.so
ipcp-accept-local
ipcp-accept-remote
idle 72000
ktune
noproxyarp
asyncmap 0
noauth
crtscts
lock
hide-password
modem
noipx

ipparam L2tpIPsecVpn-SuaVPN

promptprog "/usr/bin/L2tpIPsecVpn"

refuse-eap
refuse-pap
refuse-chap

remotename ""
name "<Seu_usuário>"
password "<Sua_Senha>"

usepeerdns
```


### Faça restart do xl2tp e ipsec para aplicar as alterações:

$ `sudo /etc/init.d/ipsec restart`

$ `sudo /etc/init.d/xl2tpd restart`

