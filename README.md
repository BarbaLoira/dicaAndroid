 
# <Strong>Dicas sobre desevolver apps android </Strong>


* Antes de destrinchar um pouco sobre algumas coisas essencias na contrução do app android aqui vai uma dica show de bola,
este site https://android-arsenal.com/tag/59?sort=rating  ele reuni implementações sobre para android com varias dicas, como exemplo se você clicar neste link ele mostrar um filtro sobre mapas, vale a pena dar uma olhada.

### 1 - Action bar

#### 1.1 -  Como tirar o action bar

<p> Basta apenas modificar no <b> AndroidManifest.xml </b> a propriedade tema do android : </p>

```xml
 android:theme="@style/AppTheme"
```

<p> que fica ta tag <b> Application </b> por esse novo tema :</p>


```xml
 android:theme="@style/Theme.AppCompat.Light.NoActionBar"
```

### 2 - Fragmentos

#### 2.1 - "CRUD" de fragmentos

Trocando de fragmento :

```java
  getFragmentManager().beginTransaction().replace(R.id.rl_content_main, new Fragment())
  .addToBackStack(null).commit();
```

Adicionando Fragmento :
  
```java
getSupportFragmentManager().beginTransaction()
.add(R.id.rl_content_main, new Fragment(),"Fragmento").addToBackStack(null).commit();
```


Removendo fragmento :

```java
        getFragmentManager().beginTransaction().remove(this)
        .add(R.id.rl_content_main, new Fragment()).addToBackStack(null).commit();
```
    
 ### 3 - ButterKnife

#### 3.1 - Adcionando em Gradle - App

```gradle
    implementation 'com.jakewharton:butterknife:8.8.1'
    annotationProcessor 'com.jakewharton:butterknife-compiler:8.8.1'
```

#### 3.2 - Como usar na classe

```java
import butterknife.BindView;
import butterknife.ButterKnife;

public class ExampleActivity extends AppCompatActivity {
   // como referenciar um compoente do fragmento ou activity
    @BindView(R.id.input_email)
    EditText _emailText;
    
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_login);
        // aqui o obj faz o bind sobre o contexto
        ButterKnife.bind(this);   
    }       
}
```
 ### 4 - Progress  (* ProgressDialog API level 26 is deprecated )
 
 É possivel colocar o progress de forma estática ou dinâmica.

#### 4.1 - Componente xml - estática

```xml
<ProgressBar
    style="@style/Widget.AppCompat.ProgressBar.Horizontal"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"/>
```

#### 4.2 - Componente xml - dinâmica


```java

RelativeLayout layout = findViewById(R.id.display); //specify here Root layout Id

(or)

RelativeLayout layout = findViewById(this);

(and)

progressBar = new ProgressBar(youractivity.this,null,android.R.attr.progressBarStyleLarge);
 RelativeLayout.LayoutParams params = new RelativeLayout.LayoutParams(100,100);
 params.addRule(RelativeLayout.CENTER_IN_PARENT);
 layout.addView(progressBar,params);
 
 progressBar.setVisibility(View.VISIBLE);  //To show ProgressBar
 progressBar.setVisibility(View.GONE);     // To Hide ProgressBar

```

para <b> desabilitar </b> a interação do usuário basta colocar:

```java
getWindow().setFlags(WindowManager.LayoutParams.FLAG_NOT_TOUCHABLE,
                           WindowManager.LayoutParams.FLAG_NOT_TOUCHABLE);
```

para <b> habilitar</b> novamente a interação do usuário:
```java
getWindow().clearFlags(WindowManager.LayoutParams.FLAG_NOT_TOUCHABLE);
```

#### 4.3 - Criando estilo para manter a cor padrão

```xml
<style name="LinearProgress" parent="Theme.AppCompat.Light">
    <item name="colorAccent">@color/indigo</item>
    <item name="android:progressBackgroundTint">@color/pink</item>
</style>
```
### 5 Mapa Offline
 

A seguir alguns links de Maps que poderão lhe ajudar sobre como manter mapa offline:

➙ Offline Maps API for Android: https://github.com/mapsme/api-android

➙ MapBox offline maps: https://www.mapbox.com/help/mobile-offline/

➙ APIs de mapa, algumas com suporte offline: https://android-arsenal.com/tag/59?sort=rating

➙ Add-ons para o Android Google Maps API v2 framework: https://github.com/cocoahero/android-gmaps-addons

➙ Conteúdo Stack Overflow de como colocar offline mode no Google Maps: https://stackoverflow.com/a/14833256/2578331


### Cores

A Google tem padrões para cores do android o site abaixo mantém este padrão e é muito facil usa-lo

https://www.materialpalette.com/


### Imagem / Foto 

### Cortar imagem

É impressendivel usar alguma biblioteca de terceiros para usar na app, pois nem todos dos dispositivos aceitam o CROP :

```java
  Intent cropIntent = new Intent("com.android.camera.action.CROP");
```

comentários do stack sobre isso : 

https://stackoverflow.com/questions/45094968/android-crop-image-using-com-android-camera-action-crop-crash-in-htc-and-google

video que super recomendo sobre o EDIMODO CROPPER :

https://www.youtube.com/watch?v=pFurCTMEiQY



## Erros e soluções

### FileUriExposedException

Este problema está relacionado ao SDK Version do android, pois da versão 24 para cima o tratamento com os arquivos foram modificados, desta forma é necessario usar o ```java FileProvider ```, abaixo segue os passos para adaptar seu codigo ao novo tratamento de arquivo:


1 ➙ Adcionar na classe que usa o arquivo a herança do   ```java FileProvider ```

     ```java
     public class GenericFileProvider extends FileProvider {} 
     ```

2 ➙ Adcionar um FileProvider tag no AndroidManifest.xml


```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    ...
    <application
        ...
        <provider
            android:name=".GenericFileProvider"
            android:authorities="${applicationId}.my.package.name.provider"
            android:exported="false"
            android:grantUriPermissions="true">
            <meta-data
                android:name="android.support.FILE_PROVIDER_PATHS"
                android:resource="@xml/provider_paths"/>
        </provider>
    </application>
</manifest>
```


3 ➙ Após fazer isto você deve criar um arquivo xml  ```java @xml/provider_paths ``` dentro de  ```java res/xml``` , talvez a pasta necessite ser criada caso não exista, o conteúdo descreve como compartilhar o acesso ao armazenamento externo a pasta raiz ```java (path=".")``` com o nome <Strong> external_files </Strong> 

```xml
  <?xml version="1.0" encoding="utf-8"?>
<paths xmlns:android="http://schemas.android.com/apk/res/android">
    <external-path name="external_files" path="."/>
</paths>
```

4 ➙ Finalmente o ultimo passo você deve modificar a forma de como recuperar o arquivo, seja ele Uri ou outro tipo de arquivo ou pasta mas a lógica é a mesma:

```java
Uri photoURI = FileProvider.getUriForFile(context, context.getApplicationContext().getPackageName() + ".my.package.name.provider", createImageFile());

```

.md Observação: Caso você queira abrir o arquivo, você necessita adcionar ao intent a seguinte <Strong>Flag</Strong>:

```java
intent.addFlags(Intent.FLAG_GRANT_READ_URI_PERMISSION);
```







 
