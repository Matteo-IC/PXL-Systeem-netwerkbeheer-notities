# Module 5

## Layer 2 loops

Een **layer 2 loop** is een **netwerk probleem** waarbij **frames** **oneindig** worden **doorgestuurd**.

Dit gebeurt wanneer **switches** met **redundante paden** bijvoorbeeld een **broadcast frame ontvangen** 
en deze **doorsturen naar** alle **andere poorten**.

Maar als het **broadcast frame** dan terugkomt bij een **switch** die het **broadcast frame al** heeft **ontvangen**,
komt het **frame** van een **andere poort** en wordt het **frame weer doorgestuurd door alle egress poorten**.\
Zo gaat het **frame** **oneindig** door en **vermenigvuldigt het zichzelf** in het **netwerk** tot deze **plat ligt**.

## STP

Het **Spanning Tree Protocol (STP)** is een **netwerk protocol** dat **layer 2 loops** **voorkomt**.

**STP** doet dit door bepaalde **poorten** **uit te schakelen**.

Doordat **STP poorten uitschakelt, voorkomt** het dat **frames gestuurd** worden naar **switches** die het
**frame al hebben ontvangen**.

### Hoe werkt STP?

**STP** moet **kiezen** welke **poorten** **uitgeschakeld** worden.

Dit gebeurt door de **poorten uit te schakelen** die **niet** het **beste pad** zijn naar de **root bridge**.\
De **root bridge** is de **switch** die het **centraal punt** voor **STP** is.




