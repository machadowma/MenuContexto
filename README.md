# MenuContexto
App Android Didático: Menu de contexto flutuante

<table>
<tr align=center>
<td><img src="https://github.com/machadowma/MenuContexto/blob/master/screen_capture_1.png" align="left" height="360" width="180" ></td>
</tr>
<tr align=center>
<td>O menu aparece ao dar um clique longo no item da ListView</td>
</tr>
</table>

Crie o Projeto com uma *Empty Activity*.



Crie um arquivo de menu (*File->New->Android Resource File*), preenchendo os campos conforme abaixo:
* *File_name = menu_contexto*
* *Resource type = menu*

Edite o arquivo *menu_contexto.xml*, incluindo os itens do menu:
```
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android">
    <item
        android:id="@+id/action_edit"
        android:title="Editar" />
    <item
        android:id="@+id/action_delete"
        android:title="Excluir" />
</menu>
```

No arquivo *activity_main.xml*, adicione uma *ListView*:
```
<ListView
        android:id="@+id/listView"
        android:layout_width="0dp"
        android:layout_height="0dp"
        android:layout_marginStart="8dp"
        android:layout_marginLeft="8dp"
        android:layout_marginTop="8dp"
        android:layout_marginEnd="8dp"
        android:layout_marginRight="8dp"
        android:layout_marginBottom="8dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />
```

Em *MainActivity.java*, declare a listView:
```
public class MainActivity extends AppCompatActivity {
    public ListView listView;
```

No método *onCreate*, instancie a listView e adicione itens:
```
listView = (ListView) findViewById(R.id.listView);

        String[] nomes = {
                "Paulo", "Pedro", "Fátima", "João",
                "Maria", "José", "Antônio", "Francisco" };

        ArrayAdapter adapter =
                new ArrayAdapter(this,
                        android.R.layout.simple_list_item_1, nomes);
        listView.setAdapter(adapter);
```

Ainda no método *onCreate* de *MainActivity.java*, registre a *listView* que estará associada ao menu de contexto chamando registerForContextMenu().
```
registerForContextMenu(listView);
```

Implemente o método onCreateContextMenu() em sua Activity.
Quando a visualização registrada receber um evento de clique longo, o sistema chamará o método .onCreateContextMenu().
É aqui que você define os itens de menu, geralmente inflando um recurso de menu:
```
@Override
    public void onCreateContextMenu(ContextMenu menu, View v,
                                    ContextMenu.ContextMenuInfo menuInfo) {
        super.onCreateContextMenu(menu, v, menuInfo);
        MenuInflater inflater = getMenuInflater();
        inflater.inflate(R.menu.menu_contexto, menu);
    }
```

Implemente onContextItemSelected().
Quando o usuário selecionar um item de menu, o sistema chamará esse método para que você possa realizar a ação adequada:
```
@Override
    public boolean onContextItemSelected(MenuItem item){
        AdapterView.AdapterContextMenuInfo info = (AdapterView.AdapterContextMenuInfo)item.getMenuInfo();
        switch (item.getItemId()) {
            case R.id.action_edit:
                Toast.makeText(this, "Editar: "+String.valueOf(info.position), Toast.LENGTH_SHORT).show();
                return true;
            case R.id.action_delete:
                Toast.makeText(this, "Excluir: "+String.valueOf(info.position), Toast.LENGTH_SHORT).show();
                return true;
        }
        return super.onContextItemSelected(item);
    }
```


# Referências
* https://developer.android.com/guide/topics/ui/menus
* https://medium.com/@nglauber/context-menu-em-listas-no-android-44f00ade5a7c
* https://www.javatpoint.com/android-context-menu-example
* https://www.alura.com.br/artigos/criando-menu-de-contexto-no-android-context-menu

# License

MIT License

Copyright (c) 2019 machadowma

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
