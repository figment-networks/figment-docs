---
description: Learn how to pull information from the Terra Blockchain using DataHub
---

# Querying the Terra blockchain

## Introduction

Often times you will need to pull information about the blockchain and its state such as:

* Most recent synced block 
* Node information 
* Validator set status 
* Token prices

Let’s see how this can be done by using DataHub to connect to a Terra node.

In this tutorial, we will explore different queries that we can run again our [**DataHub** ](https://figment.io/datahub-waitlist/)Terra node. More specifically, we will take a look at retrieving data about:

* Blockchain details
* Account details
* Luna exchange rates
* Governance proposals

## **Prerequisites**

1. Please make sure that you completed tutorials \#1 \("Connecting to a Terra node with DataHub"\) and \#2 \("Creating your first Terra account with the Terra SDK"\) before moving forward. We will be building on top of the Nodejs application created in these tutorials. 
2. Make sure that you connect to an archive Tequila node available on DataHub.

![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAA0AAAABcCAYAAABHn9U/AAABRWlDQ1BJQ0MgUHJv%20ZmlsZQAAKJFjYGASSSwoyGFhYGDIzSspCnJ3UoiIjFJgf8LAxSAMhJwM/InJxQWO%20AQE+QCUMMBoVfLvGwAiiL+uCzGKY9L+g3Km7c8+uKe+VJiQqYqpHAVwpqcXJQPoP%20EKclFxSVMDAwpgDZyuUlBSB2B5AtUgR0FJA9B8ROh7A3gNhJEPYRsJqQIGcg+waQ%20LZCckQg0g/EFkK2ThCSejsSG2gsCPC6uPj4KAUYmhmYuBJxLOihJrSgB0c75BZVF%20mekZJQqOwFBKVfDMS9bTUTAyMDJgYACFOUT15xvgsGQU40CIFc9iYLDiBgqeRYjF%20zWVg2HEU6O12hJjKfAYGXkMGhj03ChKLEuEOYPzGUpxmbARhc29nYGCd9v//53AG%20BnZNBoa/1////739//+/yxgYmG8xMBz4BgBAlWAwAH7TkwAAADhlWElmTU0AKgAA%20AAgAAYdpAAQAAAABAAAAGgAAAAAAAqACAAQAAAABAAADQKADAAQAAAABAAAAXAAA%20AAAqD8drAAAwGklEQVR4Ae2dB5wURfbHC8koSFKCgoIBVBQEc8acczrDmXP2TH9z%20jmfO6cxn1jOdOeuZFcUEIkEFRAHJUZn/+9ZabW3v7OzszuzuLPyen9mu6aqurvpW%20Ddbr9+p1o4yJk4iACIiACIiACIiACIiACIjAAkBgoQWgj+qiCIiACIiACIiACIiA%20CIiACHgCUoA0EURABERABERABERABERABBYYAlKAFpihVkdFQAREQAREQAREQARE%20QASkAGkOiIAIiIAIiIAIiIAIiIAILDAEpAAtMEOtjoqACIiACIiACIiACIiACEgB%200hwQAREQAREQAREQAREQARFYYAhIAVpghlodFQEREAEREAEREAEREAERkAKkOSAC%20IiACIiACIiACIiACIrDAEJACtMAMtToqAiIgAiIgAiIgAiIgAiLQpFgIZs/93U2a%20OsvNnD3XZTKZYlWrekRABERABERABERABERABBZwAo0aNXItmzd1bVu3cM2bFqbC%20NDJlpWBtBeVn7Piprn2bVm6RVs3cQtZAiQiIgAiIgAiIgAiIgAiIgAgUg8A8U1mm%20zZjjJk6Z4bp0bF2QElQUBWjcxGleI2uzcPNi9E91iIAIiIAIiIAIiIAIiIAIiEAF%20AlOmz/YeZ53aL1IhL98TRdkDNHPWXG/5yfemKicCIiACIiACIiACIiACIiAC1SWA%20txm6RyFSFAUo4zJyeytkFHStCIiACIiACIiACIiACIhAlQTYaoPuUYgURQEqpAG6%20VgREQAREQAREQAREQAREQATqioAUoLoirfuIgAiIgAiIgAiIgAiIgAjUOwEpQPU+%20BGqACIiACIiACIiACIiACIhAXRGQAlRXpHUfERABERABERABERABERCBeicgBaje%20h0ANEAEREAEREAEREAEREAERqCsCUoDqirTuIwIiIAIiIAIiIAIiIAIiUO8EpADV%20+xCoASIgAiIgAiIgAiIgAiIgAnVFQApQXZHWfURABERABERABERABERABOqdgBSg%20eh8CNUAEREAEREAEREAEREAERKCuCEgBqivSuo8IiIAIiIAIiIAIiIAIiEC9E5AC%20VO9DoAaIgAiIgAiIgAiIgAiIgAjUFQEpQHVFWvcRAREQAREQAREQAREQARGodwJS%20gOp9CNQAERABERABERABERABERCBuiIgBaiuSOs+IlAJgS+++MKNGzeuklydFgER%20EAEREAEREAERKCYBKUDFpFnDun777Tf3ySefuNdee63WFsJ33nmn23vvvd3+++/v%20MplMDVta/ct+/PFH368hQ4a4P/74o/oV5HnF7Nmz3cEHH+z7eNNNN+V5Ve0Ue+65%2053w74D1s2LCcN7nxxhtd3759XefOnd3IkSNzlq1J5g8//JC05fnnn69JFbpGBERA%20BERABERABOYrAiWhAM2cOdM1atQorw8L+VKVqVOnJn1Yb731qmzmhAkTvELSvn17%20t9pqq7lNNtnEL4S7devmrr322nLXx3XHrDp16uT22GMPx0J6+PDh5a6Jv1x++eXu%203//+t0MhmTZtWtLOuC7StPuUU05xKGWxrLHGGpVeE66Ly9Oe1q1bu+7du/t+9e7d%202zVp0sSddNJJ7vfff/dFiznuV155pWNu0Mds7D/44INy7b/99tvj5hY1jbJHO/gw%20xrnk66+/TrK///77JF2sBPynT5/u24LyO3ny5GJVrXpEQAREQAREQAREoEESKAkF%20qDoWieqUresRmTdvXnLLqqwdLIxRKu65557kmpD46aef3PHHH++VhVBnOIYy4fjL%20L7+4Rx55xB199NFumWWWca+88krISo6jRo1yQ4cO9d+32WYbV1ldFHj33XfdFVdc%204TbaaCP366+/JnVU1Z+koCXOOOMM3x4UrbSgqGy77bb+dHXGMldZ+sc9kZ122smt%20ssoqPh3/efTRR+OvXiEod6Kevpx88slun332cWeeeaZnXhvN+L//+z9fLXPloosu%20qo1bqE4REAEREAEREAERaDAEmpRCS5s1a+bOPvvsxDULt52gGLCY3WGHHZJm9uvX%20L0k35AQL3thic8QRR7gNN9zQffjhh+6qq67yXUNZWHfddf2iPu7r4osv7g477DA3%20a9Ys98Ybb7iPPvooyUYBGDFihOvYsWNy7tVXX03Sm266aZImseSSS7rzzjvPs3/n%20nXfc3Xff7fPZl3L99de7888/33+P/5x66qmOMYsFqxUyZ84cd/HFFydZd911l+/X%20d9995w466CCHcvfiiy866l9xxRWLMu6xcoM1LC0ob/fdd1+503AbPXq0W2KJJcqd%20r+svSy+9dIW2FbsNq6++uh9n2N98881+fLDGSURABERABERABERggSRgT9YLluGj%20JxRcR1zB+++/zyYV/zHFIM7yaVu4Zs4555yMKQe+DEdToDJmsUjKvvfeez6fvJdf%20ftmXX3755TOmPGRsQZyxxbjP32uvvTLmHpUxxSGzyCKLZMx1y9fx7bffZg488MCM%20KQj+Hj179sxQlvOVyaRJk5J2r7XWWpUVy5jikpSjn0899VS5sg8++GCSzz2RXHV/%20/vnnvu2B2TXXXFOuvt12283XR9/N+pOzrscffzy5N+yC9O/fPzlvLlXhdIWjKVFJ%20uX333bdcvu1xysCRz7/+9a9yeXypatwrXPDnCViHvk+cOLFCsTfffDPJN2U6SV93%203XUVylY1L8zalDGLSjL3TEHPHH744RnmZBBTXJN7mEUtY0pkBn7Mr8022yxjCmso%20mrntttuSeWpKYsb2LyXfn3322aQciT333DPJM+uaz6OuY489NsPcpv7tttsuY4pr%20xtwMy11rFsWkTW+99Va5PH0RAREQAREQAREQgYZEoFDdgyf/BUuhjUg3INdCePz4%208RmzHCSLubDw5WhPujO2x8FXx+Ix5LE4DGmOLA7Dgp5FI4pByDcXocyYMWPKnQt5%20HClv1ot0k/33XEpKfIEFPEjuh+KVFhQ0lJaNN97YL2jJr6pulKjQzqA0cZ1ZZJLz%20LO6RXHWNHTs2KQ+XIIEX98ilALG4Du2AFQoRSlc+kmvcK7veXAmT+zEvssmRRx6Z%20lDHrYpJmvqQl9DPbvEDJQXkL/YuPsDI3Q19drAAFJT0uSzooTGYJTOr79NNPM2aZ%20Sr7vt99+SfMoH+ow90R/HuUnnEsfUcpi7rFSfdZZZyX1KiECIiACIiACIiACDY1A%20obpHg/ODOeSQQ1zYOG6WDmdKgnv66af9HgpcwXAtsyf7th78S9j/Ygtb70pnA+wW%20WuivrU/sU+Fz6KGH+j00BCM499xzHfslkBtuuMHhQvTQQw+5q6++2pc1K4lbeeWV%20/7pBNVOfffZZcsWaa66ZpEOC9rGvpzpii+KkuCkhSRqXuiBbbrllSGY9Epzgjjvu%20SPLS7nIhA8ZpFzj29RB8gIhmpjx4TnDlHG52W2yxhVtnnXXc7rvv7vNDXYUecesK%20svbaa4dkcpw7d6679957/Xf2P+Gqh0ulKYzedZDAA+ydSku2eUEQgeC2aNYtt+uu%20uzqzLvo5wnzBZTA999hTxR6chRde2OeFecV8OvHEE9O39bxMmfLzj3lmljI/X19/%20/fWkLHuGiHo3cOBAfw7eBFyA86WXXurnzi233OIYv1122cWXiV1HayPaXNI4JURA%20BERABESgjgn8OnGK+3jwMPfTzxPc77UYcbaOuzVf3a5J48auW5cObkCfZd1i7dvU%20f9+KofEVqoWl21CZJQDLjRHzn9jKwfXhSTsuSUhsAcJFCrezWMKTfuozBSrO8hYO%20rCRTpkxJzs+YMSO5ty2kk/NxIpdlJS53wgknJHXZ/pU4q9J0PnXHlixbwPu6cBUM%20zLCeIXFd5GFp4oPVI5TlaEqYL8+fmFdcJqRjtztbrFeoK5TjHpSNrRPhJpWNe8jP%20dsS9MdR9+umnVyhi+42SfIsS5/Ntf1ly7rLLLit3TdzPeF6YIpVcwxzjexBTnr1r%20W3D5iy1ApkyHYpn7778/qQOrFJK2AHHO9lgl5bAWItQd+sk4xlZE3OiCWLTApJwp%20WOF0hmvC9Yy1RAREQAREQATmBwK/TJicue2hlzJfDh2VmTO3vPv3/NC/+aUPjM3g%20IaP8WDFmhUqhukeDsgCFSGa2kPNPvHnqnRY21xP2NxYCAzRv3jw+VS691VZblfve%20qlUrN3jwYMcTeDbs89Q+PLmnoC3ey5Wv7pcePXokl/z8889JupAEARFCG7EgYHFA%20nnnmGX80JdB16NDBp9N/eP9QWmBrbnjp0/471o+mTZuWy1thhRWS71ijsMzw3hn4%20YZEKlhMsK0S4I/Q39RQqcbjudu3aVaju4YcfTs7BhfctxRwItkHY72wSz4tvvvkm%20KUL/4iACt956a5KXTsRWKVPSk2wsOJUJVjJTzHw2Uf2w3jz55JP+u+3x8e1/4okn%20ksuxXvJJC6G/gyy66KIh6UwZStJKiIAIiIAIiEBDJoDlZ53+vdxKy3VvyN2Y79ve%20tElj12f5sjH65MthbssN+tdrnxuUAsS7cIKwmLX9GOFruSPKQCy8j6YywX0oXsxS%20jvfJ8FLNIOFeKFfFkFVXXTWpZtCgQUk6TuCixeK+sZkM81EU4ratv/76vqpx48Y5%2021fi07h/ZRPcpojaxvthjjnmGF8EJptvvnm24v4c7lUoibmEBbdt2vcfyuH2Z3tP%20HC8JRVDM8umXL5zjD20NklZ8ec8QLmRBUB7SgjslHyLSxZKeF7HCkkuZjusgHSuK%20abfBdNnwHXdN5jZKI0qkBU7wLoXk83JVxKyT/sgf2+PmFcrkxJ+JEJmPrzGbXL+H%20dB36LgIiIAIiIAKlTAC3t03XXaWUm6i2RQR69ejq3vtsSHSmfpINSgHq06dPQol9%20HOb6k3wvVoKFLhYKBOWA0NBLLbWUVxDatm1blNsQ2jsIytZRRx3lYqWIF2nuuOOO%20vghWg6oUBRSluAz7mJB43wiL6GxCH8O1FjnPW9aw0vDi1GCFyHZdZeceeOABZ+6H%20Ppu9L6Gv9O+CCy5IFCD2GxVDUE6DBAtY+M7+nFhiZYk+Bnnsscd8OO7wPdtxpZVW%20Sk6z1ywWCzDgLV5Y3cy1Lc6qcfqAAw7wCiPhumlfkKDIoiQFIYR8UIzCufQxfiFr%20fYf+TrdN30VABERABESgpgTY89NUr3aoKb46v65p0yYlsU9roTrveQE3xOoQFn63%203367e+mll7w7Gk/Kealop06d/LGAW/j64sUxT/v5jvWiOoILGMpN+oMrVZs2bfw7%20cUJ922+/vbPw2+7jjz/274TZYIMNQpazSGBJOiRY6LOJnnf2oDyhZAT3QCwH4ZoX%20XnjBX8LCf8CAAeHySo8spIOgAPE+pmxCgAbuH3/CC1gXW2yx5DyLeJQFLHK8rPSS%20Sy5JqqsqIENSsIpEly5dkhLB2hVOxO5vFircYUEMH74HCe+cCt+zHVu2bJnMPZQS%20XhYLHxQ+24/m3ejefvvtbJfW6Fzsfhjeq0Twg6DExUENGLdhw4b5uYvSy++Az0kn%20nZTcO3bhkwKUYFFCBERABERABERgQSRQ6CYkri90I1K6Dbk2w5uSkGzmtvGqkLYX%20b/rq4iAIvFslLWGzuy0o01kZ2/tRod74XuRnk3RwgfiakDb3MX8p4amrug/vrAkh%20p/Op26whGYtq5usnYAR9477pgBFxXen3FREqO7Q1hM2mwsAr5KWPBKFA6FdVZc3q%20lISB9hf9+SfXuMfl0uk4zDnBKpA4GAChq7MJ7Qj9CMEGQtuzzYs48EC4Lj6G9+vE%20QRB491GQOJR1YJstCEIoH9oS7sGcjoXgByEv29GUnqQ4oa9DGXM/TM4rIQIiIAIi%20IAINmcBNDzxf8s0fN35S5v1BQzIcJZlMMcasUN2jJC1AjRo1srVamcRpzmDJwC2N%208NexYPkgHDahipE41HWc9pn2h701lcl9993n4g3wuFlh9QhP37PVR12VnY/vE/rD%203hDqDO2Ny3C/8847zwdhCHttKqubslggTMnz1hY4IOwtCpastLUlrivNwSKpJU3B%20emUv5/Tf0+WSQqkE/WJ8jj766FRO2VcsG7Sta9euFfIDGzLidIWCqROx+xfWGQTr%20YJA99tgjJMsd4RaEPVdIrn6aQuL7lnYnxAKH+2DYexW3PU6He8XHOD8eF8rEc4O5%20lw5LTkh4LKG0KxaCNHz11Veud+/eyWkCegRJ/3bCeR1FQAREQAREQASKT2Dk6F/c%20p18NdyN/+qWolU+aOt299M4g9+XQH4pa74JQWSM00UI7OmLMRNeja/tCq6n29WZt%208BvFcempjY3dZk3wm81RMtKL02o3NscF7OHhfTS4Z/Xq1SurcpDj8qxZ7N857bTT%20fJ5ZHopSZ9Yb5ThpL3R1I0aMcLx3hg35vG8nHXAix+V5Z7FnKiz2iaAWu77lXUk1%20C/J+Icase/fuVQaEqGbVNSpOUAR7ia0jwmA62AIBKIKSZC9IdTfffHON7qGLREAE%20REAERKDUCNz87xfcEXvlfs9hfbf5wy++c598+b0bsNIybo2+yxWtOT+M+dU998Yn%20rsvi7dyOm1Z8r2TRblTkiooxZoXqHg1aASryeMxX1bGPiD0pRDfDGjC/C3u0Lrzw%20Qt9N+puO6ja/9z9X/1AK7X1T3oLJfjn2aUlEQAREQAREYH4gkM9immf9L7/7uRtl%20CsMff8xzbRZp6bbeaIBr27rslSGvvfeFG/7jONucP88t2rqV22zdvq5juzbu519/%20c8+8/rHr3qWjmzx1hps4eZq/drN1+7lmtpn/keffdc3t+Pedyl5M/vxbn/qXsW68%201spume6dE7xBAVp2qS5u7C+/uZmzZttLQTta9Lq+vh4KVtYGgjy8+PYgN9qi3c2z%20fnRo29ptvPbKzt6r456zts39/Q/vNdOqRXNrx0buqVc/dPaeHbdKr6Xc59+OdAuZ%20V9WqK/X0yhf3+XrYj+6zr0e4KdNmWPCIxq7fij3cavZyUuTOR19xrVo29wx+GDPe%20NW/WxFj0s7YNdtNnzrK+t3I7b7GWa9m8mZs5e477rylf4+0ltI0WauS6d13MbbFe%20v7w8ePIZM9+gHH8KVYAWylG3shooASwvHTt2dIR9Pu644xpoL6rXbCLOEXabPsfu%20b9WrZf4rTaAGglDAhWAPUn7mvzFWj0RABERABHITeNUUnO9/+NmxwaKtKTgoM0+8%20+L6/6M0Pv3JDRozxm8rbtlnYTZoy3T3x0vtewUC5+N0+KEdTp8/0ygrXPm1KBooS%20buzTZ852EyaVvablR1MaKI9yk02GjRpr15RtYEcZ++b7n6psw0dfDHNYerhfz26d%203PjfpniFpEnjhZLodyg5LVs083VNnzHLt2GQKTktmjXzCtKHn3/nz5H31kdfO45L%20du7glUHq/21KWWRclCr6j5LW2OqfNXuue+a1jxwKJPdAaXp/0FB/H/ihaC3eYVG3%20cMsWboQxeu39wdm6XZLnGlQY7JIkWIKNYh9L/KLMEmxi0ZvEXinCUUvKE8BFj71x%20EhEQAREQARFYUAmMHP2r7/qe267vFmnVwr3xwZduoiktLPhRSpDdt1rXKxmPPv8/%20r2T8OHZ8Yp1pYpaS/XYe6JWAfz32qr8ORaHnkp1MeRrthv8wzkdi/WPePNdu0UWS%2063zF0Z/gqsaenbc//torZX17L52zDViLkObNm7o+9rLXNVZZziteKEQD1+rjXeAW%2077hoBRe4gWaFWt7eufPQs2+bgjPdW79QzHbZYm1TWJp7a9frHwx2Y8ZN9ApPuzZ/%20vVfx7ztu5CabsgMLwlbT92+Hj3avm4IDt5mz5nhlCKVr7f69fd+feuVDN+pPzlGX%20SzYpBahkh0YNEwEREAEREAEREAERKIQA1ou5puhg0UD5QTZas+y9kuShBGHdQKFA%20sGhgZRk3YZLr1rnMkoOrXBN7uIy0NUXh14mTvdVn5V7dvQJEkAOUH6R3zyX8Mduf%20xdsv6k9zDwRrUVVtwH0NBQ6rDO5tjRdayO8j6rdCD19HZX86tm/js1DIUIDoJ33g%20JaRjf5no3enCtbjWBYETSg/ubgjubghugwhFYYOgCD1p1rIgs+fMDcmSP0oBKvkh%20UgNFQAREQAREQAREQARqQgA3NSw4KBsoQizucT3DgjOgD8GZyvJYvDdv1tS7x3Gf%202CKC61eQqdPL0ihM7BNiLxAucGw/QHr3XDIUrfRoTUokbl+2NtCOA3fdxJSgX7yl%206LuRY70bGnt8gsyb95cCE85lOw4eOsqNHjfBde3U3q2zai9fz0+2t6i6gqsg0s6O%2022+yhk+jADbyTob+a8n/kQJU8kOkBoqACIiACIiACIiACNSUQKcObf3C/xFz6cL6%20gtsblo61TQnoahHU2PCPu1enjmXlUEoIfEDQAwTrycPPveMjArMvBotRewtGgPS0%20YAffmkKFlQWlqIW5qlVXcrXhP6984K0/vXos4Tp3bGdtL9vLRHTiNn9arX61vTi4%209QXLVmX3nzJtps+aYfuWUKRGm/tbTQSLGAEU6PNHg4f5KgiugIVtX3OfawiiIAgN%20YZTURhEQAREQAREQAREQgRoR2GrD/q69uYJhyQnKz5Yb9Pd1bbH+qt6SQ5AD8rAI%20bbF+P7fwn+5yFGq9cEs31QIH4BqH4sQ1KEFIn+W6+SN/UFJqIrnasN6AFbxSxV4j%209g1xX6LAISgiWHNwYWOPTix/Ni85hVK3qrnNoaBh/fpiyKjErS0plEci1LvT5mt5%20ixmKDx9c5bbcYNU8aiiNIgqDXRrjoFaIgAiIgAiIgAiIgAhUk0B1QioTAnuWhW+O%20lZtwu3nmwoV1hzDQQQiE8KyFmu5sliEW/Ox5CdHWKMN3Fv+EuUbB2H/njWtkAQr3%20y9aGkId7HFHpwj6mcD4c2UtEG/IR+tnMQlwHJS6fayorQzhs6sF9MF+pzphVVmeh%20YbDlAlcZWZ0XAREQAREQAREQARGYbwhgvcmm/NBBXMpi5Sdbp2Plh3zcztibg6y+%20yrIFKT/UkasNKBi5lIx8lR/uUxM3Pa7LJiFIQra8Uj4nBaiUR0dtEwEREAEREAER%20EAERqBcChK3efet17X062a0bfc2lrGf3Tn7vUHipar00VDetNgHtAcqB7Nxzz3V8%200nLqqae6lVZayX+OPPLIdHbRvk+cONE9/PDD7qabbnKfffZZhXrnzJnjnn/+eXft%20tde6V155JYlAEhccNmyYu/POO93dd9/teClmZTJt2jT36KOPurfffruyIjU+v956%206yW87rrrrhrXE1+4ySabuMceeyw+1SDSJ554ojv//PPzamtl8y+vi4tcaMiQIW7t%20tdd2zKe6FObOM888U+Nb4k5AHc8991yN64gv/OKLLxy/f+rcd99946wkve2227on%20n3wy+T4/Jxakvs7P46i+iYAIZCdA2OgOFuygMqsRwQvY9yPlJzu/Uj5bcgrQYYcd%205gYOHFgSzL755hv39ddfV2jLXnvt5a6++mrXoUMHN3z48Ar5xTgxevRot/rqq7uD%20Dz7YKzj9+/d3d9xxR1L13Llz3a677uq23nprd9ttt7nNNtvMHXDAAf5lVKHQ66+/%207pZbbjl3+umn+0UbStvHH38csssdWWzvvvvu7oorrih3vhhfWPDDCwXs11/LXkZW%20aL2vvfaaGzduXKHV1Pn1zKfvvvsur/tWNv/yurjIhWbMsLc/v/++41gdGTVqlPdJ%20fuutt6pzWVL23Xffdb/8UuZekJysRgKfaOoo1rz729/+5t577z3397//3e2yyy5Z%20W/Lmm2+6sWPLXqyXtUA9nyx0TOLml3pf47YqLQIiMH8SQEmZ+/vv82fn5sNeEYo8%20vFOpPrtXci5wxFEPsdTrEwz3xvqSTfr27etP33fffUVbWKXvc+WVV/qFHwvmbt26%20eUXnkEMOcXvssYdr3bq1f6LNk/Fnn33WbbPNNu6f//ynO/nkk91BBx3kNtxwQ1/d%200Ucf7dZaay3H4hNrUefOnX0ZFKNYPvnkE8f9Flnkr7cAx/mFpjfeeONCq1ggr69s%20/jUkGCggCJaYhi4oDvwe33jjjeQ3lq1PU6dOzXa6ZM4Vc0xKva8lA10NEQERqDUC%203Tp3cENHjHErLde91u6hiotHYIiNVbcuHYpXYQ1rKhkL0BlnnOHWWGMNr3TghkWa%20z0UXXZR0jf9x33LLLQ4FhM1e5KddtnD1wtLRqVMnd95553mrBi5gQXDjiV1qcI3h%20XLxAu+CCC7yLC24utKu68tRTT/nrUVT4YKXhaX515Pbbb/cWHpQfFl64uiEvvvii%20P7I4Xnzxxb3y87s9+UAZQ4JbGAs1PkcccYS99Kupvw43NxZvY8aM8WX5w7UHHnig%20t/yssMIKyfm6TowcOdIrd4wbY7vlllsm7laM+2WXXeYVQfIvvvjiWmke9TJ3uD/c%20sb5NmlT2tuNwQxRNnv4//vjjfv5Rdvvttw/Z/o3OjN2AAQOSergmFpTRY4891s+N%20zTff3CuocX6u+XfzzTc73P/ihwRYZZjDDzzwQFINT+aZv7SvV69ejuvCwjcplCPB%20XMGiyPzl+qeffrpc6enTp3tlG07cA26XXHJJ0i4so/w+Uc4RFPPwm/7555/9ua++%20+sqz4x7UQX76PhRkvuJqRTnGJLa63n///T7PV/jnH8aDfwdiwXUNRtyHuZXLHTS+%20jjTX0jbGCjn00EP9dx5GxMJ9Yc4n/A5DfpjDzF8+zGfqe+KJJ3yRa665xv87Ac9l%20llnGXXXVVb6/e++9t8MVNkhV40o7GetsvPIZk3Cfqo65+sq1Dz74YPLvNL8FHtRI%20REAERKA2CAxYeVn3v0+HuK+++0GWoNoAXKQ6sfx8OfQH995nQ+wFtMsWqdaaV1My%20FiDcSdZZZx3v7sWC/5xzzvG9YkEQhEXBSSed5Nh3c+aZZ7p77rnHbbDBBm7y5Mmu%20TZs2DssGizYsDkcddZRfkP30008uXtjjxhO71OAawzkUIKJvICyQ+vTp46+vruLC%209Z9//rl/QozyRNvYo8PCBLeYfKwsLD759OvXj+p8X7bbbjuvuMEG+f777/2CjvR1%20113nF0krrriiGzFiBKcc/UboB21AEQp1kNe1a1efT9tmzZrljjnmGPfII4/4c3X9%2057fffnMrr7yya9WqlW8HCyYUDNgvu+yyfmF/2mmnOVwP119//WRuFLuduAeyuGUx%20P3ToUK9Aw+qFF15IbsXCGWWTPR777LOPw8r2n//8J8m//PLLHW1l4c/ilsUrZZm3%20QeDMWFx//fX+w5xlPIPkmn+wYf6/8847iRUCpZg5fO+99/oqSG+00UZuq622cg89%209JB3AeMafgecz0eOP/54r0ScddZZ/neR3guHAoTSygMK5hJuYbha8htijwzKOb9h%20lB2UFpTsMJ8XXXRR3wTmKm6k/I6bN2/uH37ssMMOvr38WxDk7LPP9gojTE855RRf%209sYbb/TZKEcoBbF88MEHbs0114xPeRdMlDDmEO2E/6BBg7xCVK5gli/8G0RfUCBQ%20XPkt4VqKQhYL7rsotzvvvLPbc8894yz38ssv+3mBm+mmm27q94Ext+gv8uOPP/qH%20OcwJ+HE/0vwuUXjhl8+4fvTRR44P7UzzymdMyjU6x5dcfcU9Fc78O8yev1tvvdXz%20/vTTT92qqzacd0Tk6L6yREAESojAYu3buB03W9N9Yi/kRBH63TyJJKVHALc3LD+M%20FWNW72JPJguW4aMnFFxHqMAWKRlb5IavydEWFvjSZPbbb7/k3MyZMzOmUGRsAeXP%202aLDf7en4/67Lcr8NbaASq6hDttLk3y3/0H7MranJjkXEjvttFOGT2ViC+DMFlts%20UVl2ct4WaP4ethfBnzMFLGMLt6wfU3wyttDy5WmbBSbwfbKFpD9nC0Bfx5JLLpnZ%20f//9M7aI9OdtgZWxRV3G9gr5fFuk+/O23yRji3TP1BZQ/pw9jfVlbNGdXMsJ23Pk%206/CZ9sesH1nbSNttYZ8xy0Ol+abshWqSI2NlT76T7yHBOcbFFm7hlD+GcVx33XUz%20yy+/fJJnFjxf/oYbbvDnqmqnWbkqbSd9YW5lE7PE+PuEdlDGFqT+3H//+98Kl5gi%206fMYh1ji65kv9DXc05Qn/932fMWX+HS2+WeKeqZnz54ZW4Qn5XfbbTc/duGELXwz%20zI94TttC28+XUCbX0dyafJtsEZ0UM/dKf86U++RcOmHKVYXfQ5if9nAiXbzC93Df%20Sy+9NMmDFf0JcsIJJ/j+h+/MHeZVLLbQz1x44YX+FGNPHbYYT4qE37wpSsm5fBL0%20nbpsIZ+zOGVMeSlXxoJflJvDZtH1dYU5TD78EMbdHgj5NO025dOn8xnXqnhRUXXG%20xN84x59sfTUlz/ctzL8wrvGczVGlskRABERABESgSgKF6h5lJg/7v1ipS7B88LQY%20NxY+LVu29JaS8ASep/a2WE4sOausskq9dItIWTzpDe5cYU/OlClTfHsIaMBT82wf%20rFw8DUfY5I8li6fdPL1FQl6zZs285QYLhClC/qkyT585H5fj6bgtsnygBJtNSR5p%20rAK2ePbX+ozUH562Z2sj53jKDffK8rt06eII1JCPfPnll94yln46HCxyWNSw/ATB%20ChJLVe0koERl7eT8//73P18dkfSwKAaXLKwfCNaOtIQxjc9jEUF48h5L6Ec4Rz5u%20iUjv3r390Ral/ljVH+Y9440VivHGukf0PnswkFyKBQDrAvcIvxXcMu9OuYUlF6QS%20WCMQgnAEwYKZFuZlcBnkPrhXxu5a6fLp73AlKl5wowsWFfoUC5aEIFg0scSYUhlO%205XWMLUr8/pB8med1gyoK4QIWz5nQhviy0H+sxCG98MILu7DPJt9xLQavuF3VTX/7%207bfOFH17m3qZgwH9ob91HUGwuu1WeREQAREQgQWHQMm4wFWFfPbs2b4IIaGJeBYL%20rlMIbmNLLbVUkhWUgeRElgTuX8UUFAsWqLjW4V6G2w/uTfjkh0XbSy+95Bev2e6L%200tS+fXufhSsVfSXcbtiLQj6yxBJLePcmFhdh4c09e/To4fMXW2wxf8T9yJ6G+4V2%20CAWMMsUCGdcpFiY77rijL4vLGR++s8BGAUBJyiYszHBfwo0om7AgDov8bPnxOcag%20bdu2rnHjxvHpcmmU3SBxmnNVtRNlrLJ2cj1udrhF2pN3726EixouTuwvYR9ZGDfK%20IjALc67sTNlfFBKEMckl7dq1S7JDn+M9aElmJQmUa9zCXn311UThiCOSsSeIOZje%20v8aY5CPsC0NatGiRFE8zR1lE+cZdiyiEBNhAWa9OtDX2wRAdkH19KFgs+lGC0yyC%20yxyNCcpkUOaTBkaJbJHq4vaHdL4KelR1jZMwDQoBlcTpUGnoG8c4HXjkO67V5RXu%20X6wjv+f074N/L4r9b22x2qt6REAEREAEFjwCJacAsWieMGFChZEIC3ueDrNgzSZs%20HibkbRCeRKbFXIPKbaIOT//T5fL5jjLy4YcfliuKMkIbzM0m2QcQAhiEgvGepHAu%20fWQ/D0EMUPhYuOL/j/AEHMEKQgAINjyjiLCPBh/7oMwEy4K5jvnIb1zDvhEElizq%20WbzGwj4OlEauZWEOKz65JF7M5ypHnrluOawxaeF+WDF41wwb7tNCH9jXEYR+xpJP%20O0Pkvvi6OM0+HRRoAhaE+ZW+T1w+W5r+IewZYvN6bQmMsM6gqKFwsNcHBSQIfYVz%206Ec4nz6isLBvCL5EAgwSxpz+E2odSYdPZ28RijSBD5ifKH/Me+qKJSz001YdyvAb%20QVFjPwnCPRiD6ggWPK7Buso+QOZQtjrC74e6gzIcPyxh0z77vxB+d/HeQ3+ywD88%20AEFpDFLducV1+Y5ruEdlx1xjEq7Bssd+NyJPYpWujvDwgD1PKKlhbvBvVWylrE59%20KisCIiACIiACxSZQci5wKDEsQLBAsJgJ73oJG+TZdE3IZhQNFByeIoeFBU/GeZJP%20mcGDB/tACWlgbEAOG8O5B59YeCqMux0fnriymArf00+MWXjidoeSwoKGxSiLKhbC%20RLPC5YPIXLanIb5FXumwGMOFDRcxrEEsTIMrWHgJIwocnHAlQth8jLAgZoM1m8RR%20HggQQTvYCM6TdiwufI8/tJ0n8JxLP8H1lRb4BwsL7HGdg5ft4fI1EgQAoW1YqWgz%20kdTCu2NQJnD/YdxZyGL9KLYErrQPFyuCGcTRAvO5H0+5sZgFyxH18AJbNt3nK/nO%20PxaTuLTBK61s2T4ZvwBlTnD/ELghBA4IbUFpYH7HQUHIQ6nFTY/oiSiGjBdzPBY2%205nMdyh7zk35nUzyCxZKN8Iwd70AKFiaiIzLGuDjiPhfmcHyfqtJEdkNYpKNApa1e%204XrGkocFLMSZ3yhvhIgPEn7r9CG0L+Tlc8RNLfw7Qfnx48f778GdkIhvISojAT6O%20O+64fKotVybfcS13UZYvucYkFGfOwCK47YbzHKvqK+9K4loesBBBL/Q1HTUvrlNp%20ERABERABEahTAvaUrmApdCNS3AA21xNcwCD4jykCSbb9TzVjC60kjzKmFGRsUePL%202FPojC0Mk3yCKZg7UiYOgkBgBNsb5MuQF+qzRY+vI2x0DvePj+TFYm55GQudnLHF%20lK/PFlg+2xY4fqN2uNZeBOrzs22cj+uL07YQzhAQItRBP22hGRfJ2KIyyaecWQTK%205Zvy6DfHhzrMnc4HNihXKPpiC8JyQRCirKIk2ehPQIbQHlNSk3pNifVjGfIYmxAU%20wfaKZNjoH/LYIE7aFvTJ9cVIWOQtP1+omzEl4ARpgiwEITCAucCFrxWObPg+/PDD%20k7ZyvVk5knKmNGdMeU2+E6SCMmEO5zv/CN7AdXzMupLUFxJsrg/5HOEZNtyHMrSD%20POZWWtgob1bIpI7APPwGGJNwjjqYO2x+z8aGeWmWoaQuUxT87ZjPBLgI7eS3ToAH%20WzgnzSHPFLHkewhgEH6vZDAmoQ7YM3b2EMRfY5ZOn0dgilAGFiEgSaiYe4R8+p5N%20wtiY8l4hm7kYro+P3AuhvaYI+3HgHP8mUc7c/3z+P/7xjwyBKhDmC799hHOmGPo0%20f6oaV+qsihf1VDYm5CHh37TQjrKzZX+r6iv/dtGfmIO5kmYI4CERAREQAREQgWIQ%20KFT3aEQj7H9UBcmIMRNdj65l+1YKqijPi9kPxBNKLBk8zUzvbcBqxAZrLDG4shBC%20lr0csWBB6t69e+JrH+cVIw1WNllzj+ByUpN6edrKxvLYXSeuJ1gMll566UrvQyhi%202tCxY8f40pJM01bGDm7pPUQ8Vae/7OmpLWFuEa4c3ul5VZ17st8BiwB7scKerupc%20X4yyuDligaAf7BmryTykD7Q/bMpPtwvXS8bEFszprLy/467HvhVTDPK+Jl2QdiC5%20XDIZW/a+8VsJe6/S9dT2d/bz8G8DbnirrbZa8iLj6ty3GONanfvVtCxWNcaWf4Pj%20/WQ1rU/XiYAIiIAIiEAgUKju0SAVoND5fI6VKUD5XKsyIiACIlAMArgL4nrHC0RR%208HHZY/8g7p6VKZfFuK/qEAEREAEREIH5kUChClDJ7QEq9iDxZDpEfSp23apPBERA%20BPIhgMUJhWfgwIE+IiSWIPY/SfnJh57KiIAIiIAIiEBxCcz3FqDi4lJtIiACIiAC%20IiACIiACIiAC9UlAFqD6pK97i4AIiIAIiIAIiIAIiIAINCgC870LXIMaDTVWBERA%20BERABERABERABESgVglIAapVvKpcBERABERABERABERABESglAhIASql0VBbREAE%20REAEREAEREAEREAEapWAFKBaxavKRUAEREAEREAEREAEREAESomAFKBSGg21RQRE%20QAREQAREQAREQAREoFYJSAGqVbyqXAREQAREQAREQAREQAREoJQISAEqpdFQW0RA%20BERABERABERABERABGqVgBSgWsWrykVABERABERABERABERABEqJgBSgUhoNtUUE%20REAEREAEREAEREAERKBWCUgBqlW8qlwEREAEREAEREAEREAERKCUCBRFAWrkGrl5%20mUwp9UttEQEREAEREAEREAEREAERmM8IoHOgexQiRVGAWrZo6qbNmFNIO3StCIiA%20CIiACIiACIiACIiACOQkgM6B7lGIFEUBatu6pZs4eYabMn22LEGFjIauFQEREAER%20EAEREAEREAERqEAAyw+6BjoHukch0ihjUkgF4drZc/9wk6bOdDNnzXUZ+08iAiIg%20AiIgAiIgAiIgAiIgAsUggNsblh+Un+ZNGxdUZdEUoIJaoYtFQAREQAREQAREQARE%20QAREoA4IFMUFrg7aqVuIgAiIgAiIgAiIgAiIgAiIQMEEpAAVjFAViIAIiIAIiIAI%20iIAIiIAINBQCUoAaykipnSIgAiIgAiIgAiIgAiIgAgUTkAJUMEJVIAIiIAIiIAIi%20IAIiIAIi0FAISAFqKCOldoqACIiACIiACIiACIiACBRMQApQwQhVgQiIgAiIgAiI%20gAiIgAiIQEMhIAWooYyU2ikCIiACIiACIiACIiACIlAwgf8HbUfOPLLQXyQAAAAA%20SUVORK5CYII=)

{% hint style="info" %}
Archive nodes allow you to query historical data, no matter how old it is.
{% endhint %}

## **Query blockchain details**

In your root directory, create a new file `query.js` and place in it below the following code snippet:

```javascript
const { LCDClient, MnemonicKey } = require('@terra-money/terra.js');
require('dotenv').config();

const main = async () => {
  const terra = new LCDClient({
    URL: process.env.TERRA_NODE_URL,
    chainID: process.env.TERRA_CHAIN_ID,
  });

  // Use key created in tutorial #2
  const mk = new MnemonicKey({
    mnemonic: process.env.MNEMONIC,
  });

  // 1. Query state of chain

  // 2. Query account information

  // 3. Query exchange rates

}

main().then(resp => {
  console.log(resp);
}).catch(err => {
  console.log(err);
})
```

This might look familiar to you. Starting from the top you can see that we import Terra.js, dotenv, and then create a new terra instance using `LCDClient`. This establishes the connection to our Terra node. Then we use `MnemonicKey`. You’ve seen this class before in tutorial \#2 where we created your account.

However, there is a subtle but very important difference in how we instantiate this class. When you want to create a random account and mnemonic, you instantiate `MnemonicKey` without any arguments. On the other hand, if you already have a mnemonic \(and we do have it in our `.env` file\) we can create a `MnemonicKey` instance from that mnemonic which will load our existing account instead of creating a new one.

Now let’s stop for a second. Do you remember we explained in tutorial \#2 that you should always keep your mnemonic secure? I hope that now you can see why this is important. The mnemonic that we stored in `.env` file allows you to recover your account using `MnemonicKey` constructor. **You should keep it private and secure at all times!**

Ok, now that we have this out of our way, let’s move on to writing our first query methods!

### Chain state

Let's start by getting more information about the Terra blockchain.

In the `query.js` file under the comment `// 1. Query state of chain` add the following code snippet below:

```javascript
const blockInfo = await terra.tendermint.blockInfo();
console.log('blockInfo: ', blockInfo);
```

This should return a response similar to:

```javascript
{
  "block_id": {
    "hash": "43D4D65924D7B10C947C385271B69B31176F9CA58BAD88E617843B1D9273D5EB",
    "parts": {
      "total": "1",
      "hash": "C11DCDC431D7B963CD435234EDD60A42084B5D9B38058854E49B6BEEBE4B17C6"
    }
  },
  "block": {
    "header": {
      "version": {
        "block": "10",
        "app": "0"
      },
      "chain_id": "tequila-0004",
      "height": "728883",
      "time": "2020-10-20T08:58:12.692826541Z",
      "last_block_id": {
        "hash": "3B7329611690F222AC7007B33ACF267B8F806ED1FDBD7D238B463398B0405949",
        "parts": {
          "total": "1",
          "hash": "32087D47AA51B7E5A142316BB63756728EB47E9A869DEA58AF37F9C85CF05796"
        }
      },
      "last_commit_hash": "46A1AF4834ECC50561414FF3ACA103815E0700E07476CC3DB5919EB4FB647208",
      "data_hash": "C42B204B512F492EF58D236D515A3CF289D31F2E0F818B28F1CD88198CF8845F",
      "validators_hash": "78FC097F4304B0D2C745B14E9FA547722881A97807BA16E03BFB0149B0758453",
      "next_validators_hash": "78FC097F4304B0D2C745B14E9FA547722881A97807BA16E03BFB0149B0758453",
      "consensus_hash": "048091BC7DDC283F77BFBF91D73C44DA58C3DF8A9CBC867405D8B7F3DAADA22F",
      "app_hash": "D1D105BB03966FF4EE800F32D2C30BCBCDE3A6066D66CD2E0CEE820AAB1D0FE3",
      "last_results_hash": "FE43D66AFA4A9A5C4F9C9DA89F4FFB52635C8F342E7FFB731D68E36C5982072A",
      "evidence_hash": "",
      "proposer_address": "090B0F80019F8BBC71FCE4C7D40C8353FB9C40E0"
    },
    "data": {
      "txs": [
        "jgbGwQI/ClLeU+EsChQtMTAwMDAwMDAwMDAwMDAwMDAwMBIEZDBlZRoEdXVzZCIUnhQdxPKyQIYbkzgMbtAR8eo0cmkqFJ4UHcTyskCGG5M4DG7QEfHqNHJpClLeU+EsChQtMTAwMDAwMDAwMDAwMDAwMDAwMBIEZjBhYxoEdWtydyIUnhQdxPKyQIYbkzgMbtAR8eo0cmkqFJ4UHcTyskCGG5M4DG7QEfHqNHJpClLeU+EsChQtMTAwMDAwMDAwMDAwMDAwMDAwMBIEY2U4YRoEdXNkciIUnhQdxPKyQIYbkzgMbtAR8eo0cmkqFJ4UHcTyskCGG5M4DG7QEfHqNHJpClLeU+EsChQtMTAwMDAwMDAwMDAwMDAwMDAwMBIEY2IyZhoEdW1udCIUnhQdxPKyQIYbkzgMbtAR8eo0cmkqFJ4UHcTyskCGG5M4DG7QEfHqNHJpCkxxWMHeChQpqZJNSwemnef35gQ6c/W750NgJBIEdXVzZBoUnhQdxPKyQIYbkzgMbtAR8eo0cmkiFJ4UHcTyskCGG5M4DG7QEfHqNHJpCkxxWMHeChTHW8UOf5FFBuw5UOPE9ygt1RRzTxIEdWtydxoUnhQdxPKyQIYbkzgMbtAR8eo0cmkiFJ4UHcTyskCGG5M4DG7QEfHqNHJpCkxxWMHeChT/g+qVp3CUH8tsMDhMKvmg/kW3lxIEdXNkchoUnhQdxPKyQIYbkzgMbtAR8eo0cmkiFJ4UHcTyskCGG5M4DG7QEfHqNHJpCkxxWMHeChSecF0kR0hoHOT/Pag2rrx484fyNxIEdW1udBoUnhQdxPKyQIYbkzgMbtAR8eo0cmkiFJ4UHcTyskCGG5M4DG7QEfHqNHJpEhQKDgoEdWtydxIGMzYwMDAwEMCaDBpqCibrWumHIQJG64Ud+sxi4ABTpaSKSjzvoCCc74+jwmM5xDJXTbjT0xJAhbwlBvcF9ehO0hUXsiKleeD88XPo5ckaAXdZ+Zqc2V8aRniDWqKyYzXmLCKdpNUmtICAQJI07H4rwuqT5EdmsA=="
      ]
    },
    "evidence": {
      "evidence": null
    },
    "last_commit": {
      "height": "728882",
      "round": "0",
      "block_id": {
        "hash": "3B7329611690F222AC7007B33ACF267B8F806ED1FDBD7D238B463398B0405949",
        "parts": {
          "total": "1",
          "hash": "32087D47AA51B7E5A142316BB63756728EB47E9A869DEA58AF37F9C85CF05796"
        }
      },
      "signatures": [
        {
          "block_id_flag": 2,
          "validator_address": "090B0F80019F8BBC71FCE4C7D40C8353FB9C40E0",
          "timestamp": "2020-10-20T08:58:12.778075272Z",
          "signature": "R5pEt8mQXy8Y1BXB3oxoma495+/R46UvVdeI/XkAOczSZJU+mMbfgoeN5lbvEaMEpZdqcfExdqLse28LFmCECA=="
        },
        {
          "block_id_flag": 2,
          "validator_address": "118BC1F7C001FEA994E356A414CB6751E3F21D82",
          "timestamp": "2020-10-20T08:58:12.692826541Z",
          "signature": "75w0zu48MBNyq/2pAWG5OirIJrcHswEr3SPV/SjGolGqHusjCDpEBufMj+HosFUIwmxmcjCFSy4c2vZpXnmMDw=="
        },
        {
          "block_id_flag": 2,
          "validator_address": "42823B42D99BF70FCAF54CFA419D03789368EE88",
          "timestamp": "2020-10-20T08:58:12.693091303Z",
          "signature": "sRrG8eQruD5jEhVwBzZJuVzkNDZDWNNqeFYaNADopy4+4OmHkmZs3mB7v5gBYsS+65rpryLENdTXayMi0HDvAQ=="
        },
        {
          "block_id_flag": 2,
          "validator_address": "47124BD026F7344E94E9A5C4700E24E3911469B1",
          "timestamp": "2020-10-20T08:58:12.849743683Z",
          "signature": "LtqHapzq8xFAR3/gJN7YAf4YQWChvbDeizbvQ6bph3LkVU2lGde+FlCDlms9erBObVG6WrkFTKxgvuPuz2VgBQ=="
        },
        {
          "block_id_flag": 2,
          "validator_address": "4AFD390FDA4DF4DD1DDA38470EC034989AC4276E",
          "timestamp": "2020-10-20T08:58:12.633376636Z",
          "signature": "+Aj6byteePsbl5RscHf/kT163vQhWec+EP8mfajyZNWhHLcf4Zp1LXJxbF6lGG+j3+DI/rq8FCaa79x/BYKABA=="
        },
        {
          "block_id_flag": 2,
          "validator_address": "5240489B9CA45F90E5DCC4F5F4398C6730DC7823",
          "timestamp": "2020-10-20T08:58:12.790334776Z",
          "signature": "fyZ+/ktI+sEpGP74NZNs49kTYf4f9d+Yft9a2nP6XnIDxcPp7qOBg7v2TgCHS6oqEgZMVV2reN4uFJr6BX8iAw=="
        },
        {
          "block_id_flag": 2,
          "validator_address": "5FFD09EC6F8511A997EA5530DB401D9B5E34FEA5",
          "timestamp": "2020-10-20T08:58:12.971736777Z",
          "signature": "Lm4+XUDgZ3HDSfpA3TiMSaUC6Lk8gYRW29xo7osn9ictqaXzrzi+lsA9ySZcjHEH0tueM2ll1vmcyDZgg1uiBg=="
        },
        {
          "block_id_flag": 2,
          "validator_address": "A38D8527D109261F1833FCEA07323B260F169A4B",
          "timestamp": "2020-10-20T08:58:12.925312277Z",
          "signature": "SsofYbJldqfQVVrvnHEWavorgVrnu1h3UpnktdbvSTGEd/XViwKQc6C1toiu09/Yd4djA1C7+DGU1T0DxICXBQ=="
        },
        {
          "block_id_flag": 2,
          "validator_address": "A4F1AE87B3C04C8A807B6D00F1D73D1CD727099C",
          "timestamp": "2020-10-20T08:58:12.973650896Z",
          "signature": "mvQZWT5asCanfmGYYq1gAsJDGttOvrkhwEDb/cnr/UY5IcOsQTtxXjsyzY7LFaGjDrWnHuwkbG4nQVG3SeRJBw=="
        },
        {
          "block_id_flag": 2,
          "validator_address": "B0DF524982C7F03C451135D0D6D53C9A8ECB0696",
          "timestamp": "2020-10-20T08:58:12.792765723Z",
          "signature": "qkazmo9qLlizWGstlLoxDhrSraA1lCzucodxOM9pR3ookGYYHQX2z0GABlIInLPiWdNFxwK8MacjxC9PenqBBw=="
        }
      ]
    }
  }
}
```

In this response, you can see that the last synced block was at height `728883` with the timestamp of `2020-10-20T08:58:12.692826541Z`. Other interesting things that can be found in the response are: `txs` \(transactions in the block\) and `signatures` \(signatures of validators who validated the block\).

### Block information

Great! Now it’s time to get some more information about the node we are connecting to. Add this snippet below the `blockInfo` call:

```javascript
const nodeInfo = await terra.tendermint.nodeInfo();
console.log('nodeInfo: ', nodeInfo);
```

You should receive a response similar to:

```javascript
{
  "node_info": {
    "protocol_version": {
      "p2p": "7",
      "block": "10",
      "app": "0"
    },
    "id": "a19b1664f34056a2c8370742468fd12115e3f95e",
    "listen_addr": "tcp://0.0.0.0:26656",
    "network": "tequila-0004",
    "version": "0.33.7",
    "channels": "4020212223303800",
    "moniker": "XRA4GiZecK",
    "other": {
      "tx_index": "on",
      "rpc_address": "tcp://0.0.0.0:26657"
    }
  },
  "application_version": {
    "name": "terra",
    "server_name": "terrad",
    "client_name": "terracli",
    "version": "0.4.0",
    "commit": "0ccb97e4427007f940b611fb0b5fb67d6a7d69f5",
    "build_tags": "netgo ledger muslc,",
    "go": "go version go1.14.7 linux/amd64"
  }
}
```

In the response, you can find information about the network name, its version, protocol version, and application version.

{% hint style="info" %}
This is very useful information to make sure that the SDK you use is compatible with the node you are connecting to.
{% endhint %}

### Validator set

Good job! Now that you have more information about the blockchain and the node, we can check what validators are in the validator set for the current height. In order to do this, add this snippet of code and run the `query.js` script:

```javascript
const validatorSet = await terra.tendermint.validatorSet();
console.log('validatorSet: ', validatorSet);
```

You should see an output similar to:

```javascript
{
  "block_height": "728915",
  "validators": [
    {
      "address": "terravalcons1py9slqqpn79mcu0uunragryr20aecs8q2va0ke",
      "pub_key": "terravalconspub1zcjduepqwgwyky5375uk0llhwf0ya5lmwy4up838jevfh3pyzf5s3hd96xjslnexul",
      "proposer_priority": "35872",
      "voting_power": "220343"
    },
    {
      "address": "terravalcons1zx9ura7qq8l2n98r26jpfjm8283ly8vzr5300n",
      "pub_key": "terravalconspub1zcjduepq7cspfkyg8wrs4yyp6w75a70p40gs22g8fe22w4uyz2mly4k72yvs5y0tlp",
      "proposer_priority": "88745",
      "voting_power": "239910"
    },
    {
      "address": "terravalcons1g2prksken0msljh4fnayr8gr0zfk3m5g0gh25z",
      "pub_key": "terravalconspub1zcjduepq85lttdmt2ela3plau0qj4ytvtxndht7dg3l58ngkg0p93am7uyqsph96vw",
      "proposer_priority": "235796",
      "voting_power": "236449"
    },
    {
      "address": "terravalcons1gufyh5px7u6ya98f5hz8qr3yuwg3g6d34ar2ys",
      "pub_key": "terravalconspub1zcjduepqh7jx8jkach39qsw0kcp9jztzwwca28tvh4s9wccypvl79x80v96qpl9lst",
      "proposer_priority": "-459891",
      "voting_power": "100"
    },
    {
      "address": "terravalcons1ft7njr76fh6d68w68prsasp5nzdvgfmwhveejd",
      "pub_key": "terravalconspub1zcjduepqnzrrsmy6dq995vnehuu63286q9nltnw6sxzq93kl8a0etgxggnms6vmu33",
      "proposer_priority": "364282",
      "voting_power": "239713"
    },
    {
      "address": "terravalcons12fqy3xuu530epewucn6lgwvvvucdc7prynxa60",
      "pub_key": "terravalconspub1zcjduepqkwv5ltsk762q2a0eaqrj4plnvjx9hkesgr47rsqphc59c9srtjnqr4y89x",
      "proposer_priority": "232828",
      "voting_power": "10"
    },
    {
      "address": "terravalcons1tl7snmr0s5g6n9l225cdksqand0rfl497ejhj6",
      "pub_key": "terravalconspub1zcjduepqsac476x64pp5pvmsrx7huag0sm96sgxqarxndscuxnjwzzr3ha2qllrlza",
      "proposer_priority": "-349080",
      "voting_power": "1904"
    },
    {
      "address": "terravalcons15wxc2f73pynp7xpnln4qwv3myc83dxjtnkue6t",
      "pub_key": "terravalconspub1zcjduepq2c7yhl7ztphp63m4k259grf86h9u7cudkd5lvgcp799px9wzkupq55z4k9",
      "proposer_priority": "-43020",
      "voting_power": "12"
    },
    {
      "address": "terravalcons15nc6apancpxg4qrmd5q0r4earntjwzvupuhd9y",
      "pub_key": "terravalconspub1zcjduepquytugqld2y8zsvk20uud9gl0ug6lhcw5vzrqequ7pysj9hacpawqrr4rkf",
      "proposer_priority": "192729",
      "voting_power": "559"
    },
    {
      "address": "terravalcons1kr04yjvzclcrc3g3xhgdd4fun28vkp5kuu0ec5",
      "pub_key": "terravalconspub1zcjduepqvyc0lm4umk8ertkgjgaldwqktkx94mtx0dcddwc0upttplgmznrs7a7n5w",
      "proposer_priority": "-298253",
      "voting_power": "11008"
    }
  ]
}
```

In this output, you can see a list of validator who are in the validator set at the most recent block, which in this case is `728915` . For every validator, most notably, you get `address` and `voting_power`. The value for the address is somehow similar to your account’s address because it also starts with `terra`. However, it is a unique address that identifies that particular validator. The value for voting power identifies how much voting power a validator has when producing blocks or voting on governance proposals \(you will find out more about proposals later in this tutorial\).

Now that we had a chance to look at validators, it's time to get more details about our own account.

In `query.js`, add this snippet below the comment `// 2. Query account information` and run the following script:

```javascript
const accountInfo = await terra.auth.accountInfo(mk.accAddress);
console.log('accountInfo: ', accountInfo);
```

This call should return an output similar to:

```javascript
{
  "type": "core/Account",
  "value": {
    "account_number": "1456",
    "address": "terra1jmn8kywcyuvg92ljvv68vmddprz2tflg33pu7g",
    "coins": [
      {
        "amount": "999971891",
        "denom": "uluna"
      }
    ],
    "public_key": {
      "type": "tendermint/PubKeySecp256k1",
      "value": "A1qIZpJ9zYJy3opUA0yjhdj20o4hK9J3QiOkr+V2CUkm"
    },
    "sequence": "2"
  }
}
```

In this response, you can see your account address and how many LUNA tokens you own. Hopefully, you see `1,000` LUNAs that you received from the testnet faucet. If your account balance is 0, please go to tutorial \#2 under “Getting testnet tokens” to request some free tokens. You will need them in tutorial \#4.

### Exchange rates

Now that we know that we own some tokens, let’s explore a call to gives more information about exchange rates to different denominations. Add this snippet to your `query.js` under `// 3. Query exchange rates`

```javascript
const exchangeRates = await terra.oracle.exchangeRates();
console.log('exchangeRates: ', JSON.stringify(exchangeRates));
```

This should return:

```javascript
[
  {
    "amount": "357.437740549741630308",
    "denom": "ukrw"
  },
  {
    "amount": "889.657532099939221897",
    "denom": "umnt"
  },
  {
    "amount": "0.222326274621939294",
    "denom": "usdr"
  },
  {
    "amount": "0.313830336202673152",
    "denom": "uusd"
  }
]
```

In this response, you see exchange rates for 4 different denominations. Get yourself familiar with those exchange rates, because in the next tutorial we will be exchanging LUNAs to different denominations.

### Governance proposals

Governance is the process by which Terra network participants can effect change for the protocol, by collectively demonstrating consensus support for proposals. In order to participate, you need to know what those proposals are. Let’s examine how we can do just that using the Terra SDK.

In `query.js` add this snippet under `// 4. Query proposals`:

```javascript
const proposals = await terra.gov.proposals();
console.log('proposals: ', JSON.stringify(proposals));
```

This should yield a response similar to:

```javascript
[
  {
    "content": {
      "type": "gov/TextProposal",
      "value": {
        "description": "Drop the power of loki.",
        "title": "test"
      }
    },
    "deposit_end_time": "2020-09-08T10:40:04.126Z",
    "final_tally_result": {
      "abstain": "0",
      "no": "0",
      "no_with_veto": "0",
      "yes": "0"
    },
    "id": "1",
    "proposal_status": "Rejected",
    "submit_time": "2020-09-07T10:40:04.126Z",
    "total_deposit": [
      {
        "amount": "11000000",
        "denom": "uluna"
      }
    ],
    "voting_end_time": "2020-09-08T10:40:04.126Z",
    "voting_start_time": "2020-09-07T10:40:04.126Z"
  },
  {
    "content": {
      "type": "gov/TextProposal",
      "value": {
        "description": "flex",
        "title": "just flexing"
      }
    },
    "deposit_end_time": "2020-10-06T11:13:30.668Z",
    "final_tally_result": {
      "abstain": "0",
      "no": "0",
      "no_with_veto": "0",
      "yes": "1009999999"
    },
    "id": "2",
    "proposal_status": "Rejected",
    "submit_time": "2020-10-05T11:13:30.668Z",
    "total_deposit": [
      {
        "amount": "512000000",
        "denom": "uluna"
      }
    ],
    "voting_end_time": "2020-10-06T11:13:30.668Z",
    "voting_start_time": "2020-10-05T11:13:30.668Z"
  },
  {
    "content": {
      "type": "gov/TextProposal",
      "value": {
        "description": "Hello?",
        "title": "Test Hello"
      }
    },
    "deposit_end_time": "2020-10-07T05:04:43.988Z",
    "final_tally_result": {
      "abstain": "0",
      "no": "0",
      "no_with_veto": "0",
      "yes": "10000000"
    },
    "id": "3",
    "proposal_status": "Rejected",
    "submit_time": "2020-10-06T05:04:43.988Z",
    "total_deposit": [
      {
        "amount": "256000000",
        "denom": "uluna"
      }
    ],
    "voting_end_time": "2020-10-07T05:04:43.988Z",
    "voting_start_time": "2020-10-06T05:04:43.988Z"
  },
  {
    "content": {
      "type": "params/ParameterChangeProposal",
      "value": {
        "changes": [
          {
            "key": "KeyMaxEntries",
            "subspace": "staking",
            "value": "100"
          }
        ],
        "description": "Test Parameter-change Proposal",
        "title": "Test"
      }
    },
    "deposit_end_time": "2020-10-14T03:13:35.869Z",
    "final_tally_result": {
      "abstain": "0",
      "no": "0",
      "no_with_veto": "0",
      "yes": "0"
    },
    "id": "4",
    "proposal_status": "Rejected",
    "submit_time": "2020-10-13T03:13:35.869Z",
    "total_deposit": [
      {
        "amount": "10000000",
        "denom": "uluna"
      }
    ],
    "voting_end_time": "2020-10-14T03:13:35.869Z",
    "voting_start_time": "2020-10-13T03:13:35.869Z"
  },
  {
    "content": {
      "type": "params/ParameterChangeProposal",
      "value": {
        "changes": [
          {
            "key": "KeyMaxEntries",
            "subspace": "staking",
            "value": "100"
          }
        ],
        "description": "Increase max entries to 100",
        "title": "Undelegation Max Entries"
      }
    },
    "deposit_end_time": "2020-10-15T12:49:21.321Z",
    "final_tally_result": {
      "abstain": "0",
      "no": "0",
      "no_with_veto": "0",
      "yes": "238449256585"
    },
    "id": "5",
    "proposal_status": "Rejected",
    "submit_time": "2020-10-14T12:49:21.321Z",
    "total_deposit": [
      {
        "amount": "100000000",
        "denom": "uluna"
      }
    ],
    "voting_end_time": "2020-10-15T12:49:21.321Z",
    "voting_start_time": "2020-10-14T12:49:21.321Z"
  },
  {
    "content": {
      "type": "gov/TextProposal",
      "value": {
        "description": "Deposit Test...",
        "title": "Deposit Test..."
      }
    },
    "deposit_end_time": "2020-10-16T07:53:04.395Z",
    "final_tally_result": {
      "abstain": "9999999",
      "no": "0",
      "no_with_veto": "0",
      "yes": "0"
    },
    "id": "6",
    "proposal_status": "Rejected",
    "submit_time": "2020-10-15T07:53:04.395Z",
    "total_deposit": [
      {
        "amount": "100000000",
        "denom": "uluna"
      }
    ],
    "voting_end_time": "2020-10-16T07:53:31.803Z",
    "voting_start_time": "2020-10-15T07:53:31.803Z"
  },
  {
    "content": {
      "type": "gov/TextProposal",
      "value": {
        "description": "Deposit!",
        "title": "Depost Test.. retry..."
      }
    },
    "deposit_end_time": "2020-10-19T05:09:58.460Z",
    "final_tally_result": {
      "abstain": "0",
      "no": "0",
      "no_with_veto": "0",
      "yes": "0"
    },
    "id": "9",
    "proposal_status": "Rejected",
    "submit_time": "2020-10-18T05:09:58.460Z",
    "total_deposit": [
      {
        "amount": "14999999",
        "denom": "uluna"
      }
    ],
    "voting_end_time": "2020-10-19T05:27:22.768Z",
    "voting_start_time": "2020-10-18T05:27:22.768Z"
  }
]
```

In this response, you can find a list of proposals. Each one comes with an ID, title, description, status, deposit, and final tally result. You can read more about governance on Terra [**here**](https://docs.terra.money/governance.html#proposals).

## **Conclusion**

Congratulations! Now you know how to query a Terra node with [**DataHub**](https://figment.io/datahub-waitlist/) to get the information you need.

For more queries please refer to the Terra documentation for the [**Tendermint RPC**](https://learn.datahub.figment.io/network-documentation/terra/rpc-and-rest-api/tendermint-rpc-1) and [**Terra LCD**](https://learn.datahub.figment.io/network-documentation/terra/rpc-and-rest-api/terra-lcd).

The complete code for this tutorial can be found [**here**](https://github.com/figment-networks/tutorials/blob/main/terra/3_query_node/query.js).

## **Next steps**

Being able to query a Terra node is fun, but wouldn’t it be great if you could not only read but also write to the blockchain? In the next tutorial, we will explore the use of transactions in order to write to the blockchain state.

If you had any difficulties following this tutorial or simply want to discuss Terra tech with us you can [**join our community today**](https://discord.gg/fszyM7K)!

