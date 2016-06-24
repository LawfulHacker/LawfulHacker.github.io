---
layout: post
title: Removing the Default Gateway from VPN on Windows 10
uname: removing-the-default-gateway-from-vpn-on-windows-10
date: 2015-12-19 10:36
author: Sergio Garcia
comments: true
categories: [VPN, Windows 10]
---

This is a simple and fast trick for those who need to access the company's VPN and doesn't want to route all your network traffic throught VPN, what can make his conection slower and allows that some restrictions can be enforeced on whats services you can access.

The Windows 10 changed several kinds of configuration from the previous versions.

In this version, you can't open IP configurations for the VPN adaptors.

Then, you can use the following commands on PowerShell to list the VPN's conections properties.

```PowerShell
Get-VpnConnection
```

A saída do comando é algo assim:

```
Name                  : Company VPN
ServerAddress         : vpn.mycompany.com
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

To make your internet traffic avoid VPN, we must set the `SplitTunneling` property to `True`, with this command:

```PowerShell
Set-VpnConnection -Name "Company VPN" -SplitTunneling $True
```

Done, now you can navigate normally while access your company's internal assets.
