1. activity_main.xml
Este archivo de diseño define la interfaz de usuario para la actividad principal de la aplicación. Aquí se utiliza un ListView para mostrar una lista de platillos típicos.

<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <ListView
        android:id="@+id/listView"
        android:layout_width="match_parent"
        android:layout_height="match_parent"/>
</LinearLayout>

![image](https://github.com/user-attachments/assets/41ac05ba-b314-422f-974a-a21c6d93ba65)

Elemento LinearLayout:

xmlns:android: Este es el espacio de nombres para los atributos de Android.
android:layout_width y android:layout_height: Se configuran como match_parent, lo que significa que el LinearLayout ocupará todo el ancho y alto de la pantalla.
android:orientation="vertical": Establece que los elementos dentro del LinearLayout se organizarán verticalmente.
Elemento ListView:

android:id="@+id/listView": Asigna un ID único al ListView, que se utilizará para referenciarlo en el código Kotlin.
android:layout_width y android:layout_height: Se configuran también como match_parent, lo que permite que el ListView ocupe toda la pantalla.

2. item_platillo.xml
Este archivo define cómo se verá cada elemento de la lista en el ListView.

<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:orientation="horizontal"
    android:padding="16dp">

    <ImageView
        android:id="@+id/platillo_icon"
        android:layout_width="48dp"
        android:layout_height="48dp"
        android:layout_marginEnd="16dp"/>

    <TextView
        android:id="@+id/platillo_nombre"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:textSize="18sp"/>
</LinearLayout>

![image](https://github.com/user-attachments/assets/9d0fc8fd-8f2d-4c7d-871c-eddc2cee7263)

Elemento LinearLayout:

android:orientation="horizontal": Esto significa que los elementos dentro de este layout se organizarán uno al lado del otro.
android:padding="16dp": Se añade un padding de 16dp (píxeles densidad-independientes) alrededor de los elementos.
Elemento ImageView:

android:id="@+id/platillo_icon": ID para identificar el icono del platillo.
android:layout_width y android:layout_height: Establece el tamaño del icono en 48dp por 48dp.
android:layout_marginEnd="16dp": Añade un margen a la derecha del icono para separar visualmente los elementos.
Elemento TextView:

android:id="@+id/platillo_nombre": ID para identificar el nombre del platillo.
android:textSize="18sp": Establece el tamaño del texto del nombre del platillo.

3. dialog_platillo.xml
Este archivo se utiliza para definir la interfaz del diálogo que muestra información detallada sobre el platillo seleccionado.

<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:orientation="vertical"
    android:padding="16dp">

    <TextView
        android:id="@+id/dialog_nombre"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:textSize="20sp"
        android:textStyle="bold"/>

    <TextView
        android:id="@+id/dialog_descripcion"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="8dp"/>

    <ImageView
        android:id="@+id/dialog_imagen"
        android:layout_width="match_parent"
        android:layout_height="200dp"
        android:scaleType="centerCrop"
        android:layout_marginTop="8dp"/>

    <Button
        android:id="@+id/dialog_compartir"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Compartir"
        android:layout_marginTop="16dp"/>

    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Cerrar"
        android:layout_marginTop="8dp"/>
</LinearLayout>

![image](https://github.com/user-attachments/assets/3165565d-025d-4612-b082-943586be8c91)

![image](https://github.com/user-attachments/assets/4ec696a6-c1bc-4570-b68a-53c337d4aa27)

Elemento LinearLayout: Similar a los anteriores, permite organizar los elementos en vertical.

Elemento TextView para el nombre del platillo:

android:id="@+id/dialog_nombre": ID para identificar el nombre en el diálogo.
android:textSize="20sp": Tamaño del texto más grande para el nombre del platillo.
android:textStyle="bold": Establece el texto en negrita.
Elemento TextView para la descripción:

android:id="@+id/dialog_descripcion": ID para identificar la descripción del platillo.
android:layout_marginTop="8dp": Margen superior para separar visualmente de otros elementos.
Elemento ImageView:

android:id="@+id/dialog_imagen": ID para identificar la imagen del platillo.
android:layout_height="200dp": Altura fija de 200dp.
android:scaleType="centerCrop": Asegura que la imagen ocupe todo el ancho y se recorte para ajustarse a la altura.
Botones:

dialog_compartir: Permite compartir información del platillo.
Cerrar: Cierra el diálogo.

4. PlatilloAdapter.kt
Esta clase se encarga de adaptar la lista de platillos para que se pueda mostrar en el ListView.

package com.example.comidastipicas

import android.content.Context
import android.view.LayoutInflater
import android.view.View
import android.view.ViewGroup
import android.widget.ArrayAdapter
import android.widget.ImageView
import android.widget.TextView

class PlatilloAdapter(context: Context, private val platillos: List<Platillo>) :
    ArrayAdapter<Platillo>(context, 0, platillos) {

    override fun getView(position: Int, convertView: View?, parent: ViewGroup): View {
        val platillo = platillos[position]

        // Verifica si se está reutilizando una vista
        val listItemView = convertView ?: LayoutInflater.from(context).inflate(R.layout.item_platillo, parent, false)

        // Referencias a los elementos del layout
        val nombreTextView: TextView = listItemView.findViewById(R.id.platillo_nombre)
        val iconoImageView: ImageView = listItemView.findViewById(R.id.platillo_icon)

        // Asignar datos
        nombreTextView.text = platillo.nombre
        iconoImageView.setImageResource(platillo.icono)

        return listItemView
    }
}

![image](https://github.com/user-attachments/assets/3060288a-d941-4a8e-a77b-66e1bafe0222)

Clase PlatilloAdapter: Esta es una subclase de ArrayAdapter que maneja la presentación de cada platillo en el ListView.

Constructor: Recibe el contexto y una lista de objetos Platillo.
Método getView: Este método es llamado para cada ítem en el ListView y se encarga de crear o reutilizar la vista.

convertView: Permite reutilizar una vista existente, mejorando el rendimiento.
LayoutInflater: Se usa para inflar el archivo de diseño item_platillo.xml.
Referencias a elementos del layout:

Obtiene el TextView y el ImageView usando sus IDs para poder asignarles datos.
Asignar datos:

Asigna el nombre y el icono del platillo a los componentes de la vista.

5. Platillo.kt
Esta es la clase de datos que representa un platillo típico.

package com.example.comidastipicas

data class Platillo(val nombre: String, val icono: Int)

![image](https://github.com/user-attachments/assets/070a154b-eb16-4c95-ade1-0b09c1b3078f)

Clase Platillo: Es una data class que contiene dos propiedades: nombre (de tipo String) y icono (de tipo Int para referirse a un recurso de imagen). 
Este diseño simplifica la creación de instancias y proporciona métodos útiles como toString().

6. MainActivity.kt
Este es el archivo de la actividad principal que contiene la lógica para mostrar la lista de platillos y manejar la interacción del usuario.

package com.example.comidastipicas

import android.content.Intent
import android.os.Bundle
import android.widget.AdapterView
import android.widget.ListView
import android.widget.Toast
import androidx.appcompat.app.AlertDialog
import androidx.appcompat.app.AppCompatActivity
import android.widget.Button
import android.widget.ImageView
import android.widget.TextView

class MainActivity : AppCompatActivity() {

    private lateinit var listView: ListView

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        listView = findViewById(R.id.listView)

        // Lista de platillos
        val platillos = listOf(
            Platillo("Tacos", R.drawable.taco_icon),
            Platillo("Sushi", R.drawable.sushi_icon),
            Platillo("Pizza", R.drawable.pizza_icon),
            Platillo("Ceviche", R.drawable.ceviche_icon),
            Platillo("Paella", R.drawable.paella_icon),
            Platillo("Biryani", R.drawable.biryani_icon),
            Platillo("Pasta", R.drawable.pasta_icon),
            Platillo("Hamburguesa", R.drawable.hamburguesa_icon),
            Platillo("Kebab", R.drawable.kebab_icon),
            Platillo("Churrasco", R.drawable.churrasco_icon)
        )


        val adapter = PlatilloAdapter(this, platillos)
        listView.adapter = adapter


        listView.onItemClickListener = AdapterView.OnItemClickListener { _, _, position, _ ->

            Toast.makeText(this, "Seleccionaste: ${platillos[position].nombre}", Toast.LENGTH_SHORT).show()


            mostrarDialogo(platillos[position])
        }
    }


    private fun mostrarDialogo(platillo: Platillo) {
        val dialog = AlertDialog.Builder(this)
        val dialogView = layoutInflater.inflate(R.layout.dialog_platillo, null)

        val nombreTextView: TextView = dialogView.findViewById(R.id.dialog_nombre)
        val descripcionTextView: TextView = dialogView.findViewById(R.id.dialog_descripcion)
        val imagenImageView: ImageView = dialogView.findViewById(R.id.dialog_imagen)
        val compartirButton: Button = dialogView.findViewById(R.id.dialog_compartir)

        nombreTextView.text = platillo.nombre
        descripcionTextView.text = when (platillo.nombre) {
            "Tacos" -> "Tortillas de maíz rellenas de carne de México."
            "Sushi" -> "Arroz envuelto en algas con pescado de Japón."
            "Pizza" -> "Masa con salsa de tomate y queso de Italia."
            "Ceviche" -> "Pescado crudo marinado en limón de Perú."
            "Paella" -> "Arroz con mariscos y verduras de España."
            "Biryani" -> "Arroz especiado con carne de India."
            "Pasta" -> "Fideos con salsa de Italia."
            "Hamburguesa" -> "Pan con carne y vegetales de Estados Unidos."
            "Kebab" -> "Carne a la parrilla envuelta en pan de India."
            "Churrasco" -> "Carne asada típica de América Latina."
            else -> ""
        }
        imagenImageView.setImageResource(platillo.icono)

        compartirButton.setOnClickListener {
            compartirPlatillo(platillo)
        }

        dialog.setView(dialogView)
        dialog.setNegativeButton("Cerrar") { dialogInterface, _ -> dialogInterface.dismiss() }
        dialog.show()
    }

    private fun compartirPlatillo(platillo: Platillo) {
        val intent = Intent().apply {
            action = Intent.ACTION_SEND
            putExtra(Intent.EXTRA_TEXT, "¡Prueba el ${platillo.nombre}!")
            type = "text/plain"
        }
        startActivity(Intent.createChooser(intent, "Compartir platillo con..."))
    }
}


![image](https://github.com/user-attachments/assets/b8e22411-c31c-4a82-be78-f2a166236c47)


![image](https://github.com/user-attachments/assets/7f8e5d4b-112d-4ab7-bd5a-f39c7e898d71)


![image](https://github.com/user-attachments/assets/1c24f355-dbb0-4f51-831e-09cbf47b2c70)

Clase MainActivity: Hereda de AppCompatActivity y es la actividad principal que maneja la interfaz de usuario.

private lateinit var listView: ListView: Se declara un ListView que se inicializa más tarde.
private lateinit var platillos: List<Platillo>: Se declara una lista de platillos.
Método onCreate: Se llama al inicio de la actividad para configurar la interfaz.

setContentView(R.layout.activity_main): Establece el diseño para la actividad.
Inicialización de datos: Crea una lista de objetos Platillo, cada uno con un nombre y un recurso de imagen correspondiente.
Configuración del ListView:

findViewById(R.id.listView): Obtiene el ListView del diseño.
PlatilloAdapter: Se crea una instancia del adaptador personalizado con la lista de platillos y se asigna al ListView.
Manejo de clics en el ListView:

setOnItemClickListener: Configura un listener que llama a mostrarDialogo cuando se selecciona un platillo.
Método mostrarDialogo:

Crea un AlertDialog que muestra el nombre, la descripción y la imagen del platillo seleccionado.
builder.setPositiveButton: Añade un botón para cerrar el diálogo.
builder.setNegativeButton: Añade un botón para compartir el platillo.
Método compartirPlatillo: Aquí puedes implementar la lógica para compartir el platillo, utilizando un Intent.



Y por ultimo este es el resultado final 

![Grabación-2024-09-29-211715](https://github.com/user-attachments/assets/25cdfdf0-50a8-40eb-84cc-b649a29367cb)





