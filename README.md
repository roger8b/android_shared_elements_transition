Compartilhamento de elementos na transição de telas.

### 1 - Habilitar a transferencia:
Dentro do arquivo styles.xml
```xml
<!-- Base application theme. -->
<style name="AppTheme" parent="Theme.AppCompat.Light.DarkActionBar">
    
<!-- enable window content transitions -->
    <item name="android:windowContentTransitions">true</item>
</style>
```

### 2 - Definir nome de transição comum para as respectivas View das duas telas:
O nome pode ser definido no xml;
```xml
...
android:transitionName="object_image"
...
```
Ou direto no java: 
```java
...
view.setTransitonName("object_image");
...
```
#### Exemplo:
***activity_home.xml***
```xml
<LinearLayout  ...>

<ImageView  android:id="@+id/iv_list_object_image"  
android:layout_width="75dp"  
android:layout_height="75dp"  
android:layout_margin="5dp"  
android:transitionName="object_image"/>
...
</LinearLayout>
```
***activity_object_detail.xml***
```xml
<LinearLayout  ...>

<ImageView  android:id="@+id/iv_list_object_image"  
android:layout_width="75dp"  
android:layout_height="75dp"  
android:layout_margin="5dp"  
android:transitionName="object_image"/>
...
</LinearLayout>
```
 ### 3 - Abrir a Activity com Transição de Elementos
Para obter o efeito de transição, você precisa especificar um conjunto de elementos e visualizações compartilhados da atividade de origem ao iniciar a atividade de destino.

#### Caso 1: Unico elemento
```java
Intent intent =  new  Intent(HomeActivity.this,  ObjectDetailActivity.class);
intent.putExtra(ObjectDetailActivity.EXTRA_OBJECT,  object);
ActivityOptionsCompat options =  
	ActivityOptionsCompat. makeSceneTransitionAnimation(this, mObjectIV,  "object_image");
 startActivity(intent, options.toBundle());
```
#### Caso 2: Multiplos Elementos
```java
Intent intent =  new  Intent(HomeActivity.this,  ObjectDetailActivity.class);
intent.putExtra(ObjectDetailActivity.EXTRA_OBJECT,  object);
Pair<View,  String> p1 =  Pair.create((View)mObjectIV,  "object_image");
Pair<View,  String> p2 =  Pair.create((View)mObjectNameTV,  "object_name");
ActivityOptionsCompat options =  
	ActivityOptionsCompat. makeSceneTransitionAnimation(this, p1, p2);
startActivity(intent, options.toBundle());
```
*Nota: Para este caso de uso certifique-se de importar "android.support.v4.util.Pair."*

