 
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
        getFragmentManager().beginTransaction().remove(this).add(R.id.rl_content_main, new Fragment()).addToBackStack(null).commit();
    ```
