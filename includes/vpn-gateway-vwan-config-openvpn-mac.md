---
 author: cherylmc
 ms.service: vpn-gateway
 ms.topic: include
 ms.date: 05/11/2022
 ms.author: cherylmc

#Customer intent: this file is used for both virtual wan and vpn gateway articles.
---

> [!IMPORTANT]
>Only MacOS 10.13 and above is supported with OpenVPN protocol.

1. Download and install an OpenVPN client, such as [TunnelBlick](https://tunnelblick.net/downloads.html).
1. Download the VPN client profile package from the Azure portal, or use the 'New-AzVpnClientConfiguration' cmdlet in PowerShell.
1. Unzip the profile. Open the vpnconfig.ovpn configuration file from the OpenVPN folder in a text editor.
1. Fill in the P2S client certificate section with the P2S client certificate public key in base64. In a PEM formatted certificate, you can open the .cer file and copy over the base64 key between the certificate headers. Use the following article links for information about how to export a certificate to get the encoded public key:

   * [VPN Gateway](../articles/vpn-gateway/vpn-gateway-certificates-point-to-site.md#cer) instructions
   * [Virtual WAN](../articles/virtual-wan/certificates-point-to-site.md#cer) instructions

1. Fill in the private key section with the P2S client certificate private key in base64. See the [Export your private key](https://openvpn.net/community-resources/how-to/#pki) on the OpenVPN site for information about how to extract a private key.
1. Don't change any other fields. Use the filled in configuration in client input to connect to the VPN.
1. Double-click the profile file to create the profile in Tunnelblick.
1. Launch Tunnelblick from the applications folder.
1. Click on the Tunnelblick icon in the system tray and pick connect.
