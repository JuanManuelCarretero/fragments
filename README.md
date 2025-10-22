
# Codelab: Navegación con Fragments en Android

**Objetivo de la práctica:**  
Trabajar con **Fragments** y el componente **Navigation** para implementar un flujo de onboarding en una app Android.



---

## 1. Introducción a los Fragments

Un **Fragment** representa un comportamiento o una parte de la interfaz de usuario en una **Activity**.  

- Se pueden combinar múltiples fragments en una sola activity para crear interfaces multipanel.  
- Un fragment puede reutilizarse en distintas activities.  
- Tiene su propio ciclo de vida y puede recibir eventos de entrada independientes.  
- Se puede agregar o quitar dinámicamente mientras la activity se está ejecutando.  

En esta práctica programaremos un **proceso de onboarding**.

---

## 2. Componentes clave del Navigation Component

1. **Navigation Graph (XML)**  
   Contiene todos los destinos de la app y las rutas posibles entre ellos.  

2. **NavHostFragment (Layout XML)**  
   Widget donde se muestran los distintos destinos del grafo de navegación.  

3. **NavController (Objeto Java/Kotlin)**  
   Gestiona el intercambio de fragments en el NavHostFragment según el usuario navega.

---

## 3. Crear el proyecto

1. Abre Android Studio y selecciona **Empty Activity** como plantilla para la MainActivity.  
2. Añade las dependencias de Navigation:

```gradle
dependencies {
    implementation "androidx.navigation:navigation-fragment:2.3.0"
    implementation "androidx.navigation:navigation-ui:2.3.0"
}
```

---

## 4. Crear el Navigation Graph

1. Haz clic derecho en `res` → **New → Android Resource File**.  
2. Nombre: `nav_graph`  
3. Resource type: **Navigation** → OK

---

## 5. Añadir fragments al Navigation Graph

Crea los fragments:  

- `Onboarding1Fragment`  
- `Onboarding2Fragment`  
- `HomeFragment`  

> `Onboarding1Fragment` será el **Start Destination**.

---

## 6. Conectar los destinos

Crea acciones de navegación:

```xml
<action
    android:id="@+id/action_onboarding1Fragment_to_onboarding2Fragment"
    app:destination="@id/onboarding2Fragment"/>

<action
    android:id="@+id/action_onboarding2Fragment_to_homeFragment"
    app:destination="@id/homeFragment"/>
```

---

## 7. Añadir el NavHost

`res/layout/activity_main.xml`:

```xml
<androidx.constraintlayout.widget.ConstraintLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <androidx.fragment.app.FragmentContainerView
        android:name="androidx.navigation.fragment.NavHostFragment"
        android:id="@+id/nav_host_fragment"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        app:defaultNavHost="true"
        app:navGraph="@navigation/nav_graph" />
</androidx.constraintlayout.widget.ConstraintLayout>
```

---

## 8. Diseñar las pantallas

### 8.1 Añadir las imágenes

Añadid las imagenes para vuestras layout en drawable. 

Añádelas en `res/drawable` como **Vector Asset**.

---

### 8.2 Layout Onboarding1Fragment

`res/layout/fragment_onboarding1.xml`:

```xml
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#4CAF50"
    android:padding="32dp">

    <ImageView
        android:id="@+id/imagen"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:adjustViewBounds="true"
        android:src="@drawable/ic_onboarding1"
        app:layout_constraintBottom_toTopOf="@+id/texto"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"/>

    <TextView
        android:id="@+id/texto"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="¡Discover the garlic soup!"
        android:textColor="#FFFFFF"
        android:textSize="30sp"
        app:layout_constraintBottom_toTopOf="@+id/botonSiguiente"
        app:layout_constraintTop_toBottomOf="@id/imagen"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"/>

    <Button
        android:id="@+id/botonSiguiente"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:backgroundTint="#FFEB3B"
        android:text="Next"
        app:layout_constraintTop_toBottomOf="@id/texto"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent" />
</androidx.constraintlayout.widget.ConstraintLayout>
```

---

### 8.3 Layout Onboarding2Fragment

`res/layout/fragment_onboarding2.xml`:

```xml
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#00BCD4"
    android:padding="32dp">

    <ImageView
        android:id="@+id/imagen"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:adjustViewBounds="true"
        android:src="@drawable/ic_onboarding2"
        app:layout_constraintBottom_toTopOf="@+id/texto"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <TextView
        android:id="@+id/texto"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="¡Blow and make bottles!"
        android:textColor="#FFFFFF"
        android:textSize="30sp"
        app:layout_constraintBottom_toTopOf="@+id/botonFinalizar"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintTop_toBottomOf="@id/imagen" />

    <Button
        android:id="@+id/botonFinalizar"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:backgroundTint="#FFC107"
        android:text="Finish"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintTop_toBottomOf="@id/texto" />
</androidx.constraintlayout.widget.ConstraintLayout>
```
## 9. Implementar la Navegación

### 9.1 Navegación Onboarding1Fragment.java
```java
public class Onboarding1Fragment extends Fragment {

    private FragmentOnboarding1Binding binding;
    private NavController navController;

    @Override
    public View onCreateView(@NonNull LayoutInflater inflater, ViewGroup container,
                             Bundle savedInstanceState) {
        return (binding = FragmentOnboarding1Binding.inflate(inflater, container, false)).getRoot();
    }

    @Override
    public void onViewCreated(@NonNull View view, @Nullable Bundle savedInstanceState) {
        super.onViewCreated(view, savedInstanceState);

        navController = Navigation.findNavController(view);

        binding.botonSiguiente.setOnClickListener(v ->
                navController.navigate(R.id.action_onboarding1Fragment_to_onboarding2Fragment)
        );
    }
}
```

### 9.2 Navegación Onboarding1Fragment.java
```java
public class Onboarding2Fragment extends Fragment {

    private FragmentOnboarding2Binding binding;
    private NavController navController;

    @Override
    public View onCreateView(@NonNull LayoutInflater inflater, ViewGroup container,
                             Bundle savedInstanceState) {
        return (binding = FragmentOnboarding2Binding.inflate(inflater, container, false)).getRoot();
    }

    @Override
    public void onViewCreated(@NonNull View view, @Nullable Bundle savedInstanceState) {
        super.onViewCreated(view, savedInstanceState);

        navController = Navigation.findNavController(view);

        binding.botonFinalizar.setOnClickListener(v ->
                navController.navigate(R.id.action_onboarding2Fragment_to_homeFragment)
        );
    }
}
```

## 10 Añadir Animaciones

### 10.1 Crear animaciones en res/anim/

slide_in_right.xml

```xml
<set xmlns:android="http://schemas.android.com/apk/res/android">
    <translate android:fromXDelta="100%" android:toXDelta="0%" android:duration="700"/>
</set>
```

slide_out_left.xml

```xml
<set xmlns:android="http://schemas.android.com/apk/res/android">
    <translate android:fromXDelta="0%" android:toXDelta="-100%" android:duration="700"/>
</set>
```
slide_in_left.xml

```xml
<set xmlns:android="http://schemas.android.com/apk/res/android">
    <translate android:fromXDelta="-100%" android:toXDelta="0%" android:duration="700"/>
</set>
```
slide_out_right.xml

```xml
<set xmlns:android="http://schemas.android.com/apk/res/android">
    <translate android:fromXDelta="0%" android:toXDelta="100%" android:duration="700"/>
</set>
```

### 10.2 Asignar navegaciones en nav_graph.xml
```xml
<action
    android:id="@+id/action_onboarding1Fragment_to_onboarding2Fragment"
    app:destination="@id/onboarding2Fragment"
    app:enterAnim="@anim/slide_in_right"
    app:exitAnim="@anim/slide_out_left"
    app:popEnterAnim="@anim/slide_in_left"
    app:popExitAnim="@anim/slide_out_right"/>

<action
    android:id="@+id/action_onboarding2Fragment_to_homeFragment"
    app:destination="@id/homeFragment"
    app:enterAnim="@anim/slide_in_right"
    app:exitAnim="@anim/slide_out_left"
    app:popEnterAnim="@anim/slide_in_left"
    app:popExitAnim="@anim/slide_out_right"/>
```