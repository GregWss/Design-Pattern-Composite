# Première étape.

Premièrement on crée l'interface qui sera implémentez par toutes les autres classes.

```java runnable
public interface Composant {

    public float getPoids();

}
```

# Deuxiéme étape.

Ensuite on crée les différentes classes que l'on pourra composer.

```java runnable
public class Remorque implements Composant {

	private int poids;
   
    public Remorque(int poids) {
		this.poids = poids;
    }
	
	@Override
    public String getPoids() {
        return this.poids;
    }

}

public class Tracteur implements Composant {

	private int poids;
   
    public Tracteur(int poids) {
		this.poids = poids;
    }
	
	@Override
    public String getPoids() {
        return this.poids;
    }
}
```

# Troisième étape.

Puis, on implémente la classe composite Composite, avec les méthodes add et remove qui permettront d'ajouter ou de supprimer plusieurs éléments à une composition.

```java runnable
public class CamionComposite implements Composant {

	private Collection children;

    public CamionComposite() {
        children = new ArrayList();
    }

  
    public void add(Composant composant){
     
        children.add(produit);
    }

  
    public void remove(Produit produit){
        children.remove(produit);
    }

    public Iterator getChildren() {
        return children.iterator();
    }
	
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

public interface Composant {

    public float getPoids();

}

public class Remorque implements Composant {

	private int poids;
   
    public Remorque(int poids) {
		this.poids = poids;
    }
	
	@Override
    public String getPoids() {
        return this.poids;
    }

}

public class Tracteur implements Composant {

	private int poids;
   
    public Tracteur(int poids) {
		this.poids = poids;
    }
	
	@Override
    public String getPoids() {
        return this.poids;
    }
}

public class CamionComposite implements Composant {

	private Collection children;

    public CamionComposite() {
        children = new ArrayList();
    }

  
    public void add(Composant composant){
     
        children.add(produit);
    }

  
    public void remove(Produit produit){
        children.remove(produit);
    }

    public Iterator getChildren() {
        return children.iterator();
    }
	
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
		System.out.println(maRemorque.getPoids());
		Tracteur monTracteur = new Tracteur(8);
		System.out.println(monTracteur.getPoids());

		CamionComposite semiRemorque = new CamionComposite();
		semiRemorque.add(maRemorque);
		semiRemorque.add(monTracteur);
		System.out.println(semiRemorque.getPoids());
	 }
}
```

