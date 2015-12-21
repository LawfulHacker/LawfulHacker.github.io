---
layout: post
title: Removendo o Default Gateway da VPN no Windows 10
uname: removing-the-default-gateway-from-vpn-on-windows-10
date: 2015-12-19 10:36
author: Sergio Garcia
comments: true
categories: [VPN, Windows 10]
---

Está é uma dica bem simples e rápida para quem acessa a VPN do trabalho mas
não quer que seu tráfego de internet seja routeado pela conexão VPN, o que
além de deixar mais lento seu acesso de internet faz com que certas restrições
possam ser impostas quais serviços você pode acessar.

O Windows 10 alterou diversas formas de configuração em relação as versões
anteriores.

Nesta versão, não é possivel abrir as configurações de IP para os adaptadores
do tipo VPN.

Assim, você pode usar os seguintes comando no PowerShell para listar as
propriedades de suas conexões VPN:

```PowerShell
Get-VpnConnection
```

A saída do comando é algo assim:

```
Name                  : VPN MinhaEmpresa
ServerAddress         : vpn.minhaempresa.com.br
AllUserConnection     : False
Guid                  : {BA67A6DF-FF27-4AAB-82BB-81A88C432605}
TunnelType            : Pptp
AuthenticationMethod  : {MsChapv2}
EncryptionLevel       : Required
L2tpIPsecAuth         :
UseWinlogonCredential : False
EapConfigXmlStream    :
ConnectionStatus      : Disconnected
RememberCredential    : False
SplitTunneling        : False
DnsSuffix             :
IdleDisconnectSeconds : 0
```

Para fazer com que o tráfego de internet não passe pela VPN, devemos
configurar a propriedade `SplitTunneling` para `True`, fazemos isso assim:

```PowerShell
Set-VpnConnection -Name "VPN MinhaEmpresa" -SplitTunneling $True
```

Pronto, agora você pode navegar normalmente enquanto acessa os recursos
internos da rede da sua empresa.
