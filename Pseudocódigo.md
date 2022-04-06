PSEUDOCÓDIGO (Wollok) MACOWINS

```java
class Nueva() {
	method precio(precioOriginal) = precioOriginal
}

class Promocion() {
	var descuento
	method precio(precioOriginal) = precioOriginal - descuento
}

class Liquidacion() {
	method precio(precioOriginal) = precioOriginal * 0.5
}

class tipoDePrenda {
	var nombre
	method precio() = ???
	/* Ahí iría qué precio corresponde a cada tipo de prenda. Ej: $100 a los sacos, $80 a los pantalones, $200 a las camisas. */
}

class Prenda {
	var estado = new Nueva()
	var tipoDePrenda
	method precio() = self.estado.precio(self.tipoDePrenda.precio())
}

class PrendaVendida {
	var prenda = new Prenda()
	var cantidad
}

class Venta {
	var prendasVendidas = []
	var tipoDeVenta // Sería new Efectivo() o new Tarjeta()
	method importeTotal() = tipoDeVenta().precio(self.prendasVendidas().sum({prenda => prenda.cantidad}), prendasVendidas)
}

class Efectivo() {
	method precio(precioOriginal, prendasVendidas) = precioOriginal 
}

class Tarjeta inherits Efectivo() {
	var cantidadDeCuotas
	const coeficienteFijo
	override method precio(precioOriginal, prendasVendidas) = precioOriginal + (cantidadDeCuotas * coeficienteFijo + prendasVendidas().sum({prendaVendida => prendaVendida().prenda().precio * 0.01}))
}

class Dia {
	var ventasDelDia = []
	method calcularGanancias = self.ventasDelDia().sum({venta => venta.importeTotal()})
}
```