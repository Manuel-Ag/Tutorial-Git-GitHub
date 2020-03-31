---
layout: post
title:  "Ejemplo RadioButton y Checkbox"
date:   2019-10-3 14:30:00 +0200
categories: primer_trimestre
order: 2
parent: Primer trimestre Android
---

# Ejemplo RadioButton y Checkbox

**Ejemplo de clase**: <https://github.com/Manuel-Ag/PMD_19-20/tree/master/RadioButtonyCheckBox>

En este ejemplo hemos aprendido a utilizar los *RadioButton* y los *CheckBox*, tanto accediendo únicamente al valor seleccionado como añadiendo un *listener* a la vista.

Para acceder a la selección del radioButton con un botón:

{% highlight java %}
public void  mostrarValores(View v) {
        String texto;
        RadioButton radioButton;
        //Referencia al RadioGroup
        RadioGroup radioGroup = findViewById(R.id.radioGroupEquipos);
        //Obtengo la id del radioButton que está seleccionado por el usuario
        int id = radioGroup.getCheckedRadioButtonId();
        //switch según el id seleccionado
        switch (id){
            case R.id.radioButtonReal:
                Toast.makeText(this, "Hala Madrid!", Toast.LENGTH_SHORT).show();
                break;
            case R.id.radioButtonAtletico:
                Toast.makeText(this, "Aupa Atleti", Toast.LENGTH_SHORT).show();
                break;
            case R.id.radioButtonZaragoza:
                Toast.makeText(this, "Viva Zaragoza" + comprobarCheckBox(), Toast.LENGTH_SHORT).show();
                break;
        }
}
{% endhighlight %}


Si queremo añadir un *listener* que reaccione cuando el usuario cambie la selección, tenemos que implementar la interface *correspondiente*:

{% highlight java %}
implements RadioGroup.OnCheckedChangeListener
{% endhighlight %}

Añadir el *listener* al componente:

{% highlight java %}
RadioGroup radioGroup = findViewById(R.id.radioGroupEquipos);
radioGroup.setOnCheckedChangeListener(this);
{% endhighlight %}

E implementar la funcionalidad del método:

{% highlight java %}
public void onCheckedChanged(RadioGroup group, int checkedId) {
        //Referencio el radioButton seleccionado
        RadioButton radioButton = findViewById(checkedId);
        //Imprimir texto del radioButon seleccionado
        Toast.makeText(this, radioButton.getText().toString(), Toast.LENGTH_SHORT).show();
}
{% endhighlight %}

Comprueba el ejemplo de GitHub y comprueba la similitud de este ejemplo de *RadioButton* en el caso de los *CheckBox*.
