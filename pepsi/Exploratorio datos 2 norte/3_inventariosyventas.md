% 17-oct-2013
% Cálculo de inventarios y ventas para clientes agrupados por tipo para la zona norte de pepsi y 3 productos
% Makefile: pandoc -s -V geometry:margin=0.7in -V lang=spanish 3_inventariosyventas.md -o InventariosVentas.pdf

Después de filtrar en el exploratorio los sku's colados y después de hacer en seriesdetiempo 
las agrupaciones por fecha y tipo de cliente, en este archivo ahora se trata de producir 
un archivo con las ventas y devoluciones promedio de cada tipo de cliente y de cada fecha. 
Después, con estos promedios, calcularemos inventarios y ventas a consumidores finales.

**NOTA IMPORTANTE:** Para calcular los inventarios de los clientes (tienditas) y sus ventas a los
consumidores (gente que compra papas en las tienditas), estamos tomando valor absoluto de ventas y 
devoluciones porque hay valores negativos. Suponemos que tiene que ver con promociones en las que la
gente llega al OXXO y canjea un cupón de "papitas gratis". No nos importa distinguir entre papas 
consumidas y pagadas y papas consumidas y gratis porque al final es demanda de papas. Quizá tenga más
sentido omitir los valores negativos, pero a mí me late que no.

Sabritas normales
--------------------------------------------------------------------------------------------------


```r
setwd("/Users/PandoraMac/Documents/David/pepsi2/Datos Norte 3 papitas/")
nombres <- c("tipo_cliente", "fecha", "vta_din", "vta_uni", "dev_din", "dev_uni")
s <- as.data.frame(read.table("papas_agregados_tipo.csv", sep = ",", header = TRUE, 
    colClasses = c(rep("character", 2), rep("numeric", 4))))
names(s) <- nombres
s2 <- s[order(s$fecha), ]
datos <- subset(s2, s$tipo_cliente != "")
datos$tipo_cliente[datos$tipo_cliente == "CINE / TEATRO"] <- "CINE_TEATRO"
datos$tipo_cliente[datos$tipo_cliente == "LONCHERIA / FOND"] <- "LONCHERIA_FONDA"
length(table(datos$tipo_cliente))

par(mfrow = c(5, 1))
myfunction <- function(x) {
    png(file = paste("/Users/PandoraMac/Documents/David/nadro_pepsi_git/pepsi/Exploratorio datos 2 norte/images/papas/ts", 
        paste(unlist(strsplit(x$tipo_cliente[1], " ")), collapse = ""), ".png", 
        sep = ""))
    plot(ts(x[, c(4, 6)]), plot.type = c("single"), col = c("blue", "red"), 
        main = x$tipo_cliente[1])
    # axis(1,at=1:nrow(x),labels=x$fecha,las=1)
    dev.off()
}
by(datos, datos$tipo_cliente, myfunction)
par(mfrow = c(1, 1))
```



Fritos
--------------------------------------------------------------------------------------------------


```r
setwd("/Users/PandoraMac/Documents/David/pepsi2/Datos Norte 3 papitas/")
nombres <- c("tipo_cliente", "fecha", "vta_din", "vta_uni", "dev_din", "dev_uni")
s <- as.data.frame(read.table("fritos_agregados_tipo.csv", sep = ",", header = TRUE, 
    colClasses = c(rep("character", 2), rep("numeric", 4))))
names(s) <- nombres
s2 <- s[order(s$fecha), ]
datos <- subset(s2, s$tipo_cliente != "")
datos$tipo_cliente[datos$tipo_cliente == "CINE / TEATRO"] <- "CINE_TEATRO"
datos$tipo_cliente[datos$tipo_cliente == "LONCHERIA / FOND"] <- "LONCHERIA_FONDA"
length(table(datos$tipo_cliente))

myfunction <- function(x) {
    png(file = paste("/Users/PandoraMac/Documents/David/nadro_pepsi_git/pepsi/Exploratorio datos 2 norte/images/fritos/ts", 
        paste(unlist(strsplit(x$tipo_cliente[1], " ")), collapse = ""), ".png", 
        sep = ""))
    plot(ts(x[, c(4, 6)]), plot.type = c("single"), col = c("blue", "red"), 
        main = x$tipo_cliente[1])
    # axis(1,at=1:nrow(x),labels=x$fecha,las=1)
    dev.off()
}
by(datos, datos$tipo_cliente, myfunction)
```



Churrumais
--------------------------------------------------------------------------------------------------


```r
setwd("/Users/PandoraMac/Documents/David/pepsi2/Datos Norte 3 papitas/")
nombres <- c("tipo_cliente", "fecha", "vta_din", "vta_uni", "dev_din", "dev_uni")
s <- as.data.frame(read.table("churrumais_agregados_tipo.csv", sep = ",", header = TRUE, 
    colClasses = c(rep("character", 2), rep("numeric", 4))))
names(s) <- nombres
s2 <- s[order(s$fecha), ]
datos <- subset(s2, s$tipo_cliente != "")
datos$tipo_cliente[datos$tipo_cliente == "CINE / TEATRO"] <- "CINE_TEATRO"
datos$tipo_cliente[datos$tipo_cliente == "LONCHERIA / FOND"] <- "LONCHERIA_FONDA"
length(table(datos$tipo_cliente))

myfunction <- function(x) {
    png(file = paste("/Users/PandoraMac/Documents/David/nadro_pepsi_git/pepsi/Exploratorio datos 2 norte/images/churrumais/ts", 
        paste(unlist(strsplit(x$tipo_cliente[1], " ")), collapse = ""), ".png", 
        sep = ""))
    plot(ts(x[, c(4, 6)]), plot.type = c("single"), col = c("blue", "red"), 
        main = x$tipo_cliente[1])
    # axis(1,at=1:nrow(x),labels=x$fecha,las=1)
    dev.off()
}
by(datos, datos$tipo_cliente, myfunction)
```
