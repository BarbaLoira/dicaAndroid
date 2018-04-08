 
# <Strong>Dicas sobre desevolver apps android </Strong>


### 1 - Layout Customizados

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
    
 ### 2 - ButterKnife

#### 2.1 - Adcionando em Gradle - App

```gradle
    implementation 'com.jakewharton:butterknife:8.8.1'
    annotationProcessor 'com.jakewharton:butterknife-compiler:8.8.1'
```

#### 2.2 - Como usar na classe

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


