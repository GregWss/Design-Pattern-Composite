# Première étape.

Premièrement on crée l'interface qui sera implémentée par toutes les autres classes.

```java Runnable
public interface Composant {

    public int getPoids();

}
```

# Deuxiéme étape.

Ensuite on crée les différentes classes que l'on pourra composer.

```java Runnable
public class Remorque implements Composant {

	private int poids;
   
    public Remorque(int poids) {
		this.poids = poids;
    }
    
    @Override
    public int getPoids() {
        return this.poids;
    }

}

public class Tracteur implements Composant {

	private int poids;
   
    public Tracteur(int poids) {
		this.poids = poids;
    }
	
	@Override
    public int getPoids() {
        return this.poids;
    }
}
```

# Troisième étape.

Puis, on implémente la classe composite Composite, avec les méthodes add et remove qui permettront d'ajouter ou de supprimer plusieurs éléments à une composition.

```java Runnable
public class CamionComposite implements Composant {

	private Collection children;

    public CamionComposite() {
        children = new ArrayList();
    }

  
    public void add(Composant composant){
     
        children.add(composant);
    }

  
    public void remove(Composant composant){
        children.remove(composant);
    }

    public Iterator getChildren() {
        return children.iterator();
    }
	
	@Override
    public int getPoids() {
        int result = 0;
        for (Iterator i = children.iterator(); i.hasNext(); ) {
            Object objet = i.next();
			
            Composant composant = (Composant)objet;

            result += composant.getPoids();
        }
        return result;
    }
}
```

# Quatrième étape.

Maintenant on implémente le main pour utiliser le Composite

```java runnable

// { autofold

import java.util.*;

interface Composant {

    public int getPoids();

}

class Remorque implements Composant {

	private int poids;
   
    public Remorque(int poids) {
		this.poids = poids;
    }
	
    @Override
    public int getPoids() {
        return this.poids;
    }

}

class Tracteur implements Composant {

	private int poids;
   
    public Tracteur(int poids) {
		this.poids = poids;
    }

    @Override
    public int getPoids() {
        return this.poids;
    }
}

class CamionComposite implements Composant {

	private Collection children;

    public CamionComposite() {
        children = new ArrayList();
    }

  
    public void add(Composant composant){
     
        children.add(composant);
    }

  
    public void remove(Composant composant){
        children.remove(composant);
    }

    public Iterator getChildren() {
        return children.iterator();
    }
	
    @Override
    public int getPoids() {
        int result = 0;
        for (Iterator i = children.iterator(); i.hasNext(); ) {
            Object objet = i.next();
			
            Composant composant = (Composant)objet;

            result += composant.getPoids();
        }
        return result;
    }
}

// }

public class Main
{

     public static void main(String[] args)
     {
		Remorque maRemorque = new Remorque(11);
		System.out.println("Le poids de ma remorque est:");
		System.out.println(maRemorque.getPoids());
	    System.out.println("tonnes");

		
		Tracteur monTracteur = new Tracteur(8);
		System.out.println("Le poids de mon tracteur est:");
		System.out.println(monTracteur.getPoids());
		System.out.println("tonnes");


		CamionComposite semiRemorque = new CamionComposite();
		semiRemorque.add(maRemorque);
		semiRemorque.add(monTracteur);
		System.out.println("Le poids de mon semi-remorque est:");
		System.out.println(semiRemorque.getPoids());
		System.out.println("tonnes");
	 }
}
```

