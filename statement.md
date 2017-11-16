# Introduction

Bienvenue sur ce tuto du design pattern Composite !

# Code

public interface Produit {

    /**
     * Fournit le prix du produit.
     * Peut être calculé.
     */
    public float getPrix();
    /**
     * Code barre unique d'un produit.
     */
    public String getCodeBarre();
    /**
     * Descriptif du produit. Peut être le résultat d'une accumulation de 
     * descriptifs si le produit est composé
     */
    public String getDescriptif();

}

public class Barre implements Produit {

    /** Creates a new instance of haltere */
    public Barre() {
    }

    /** Code barre unique d'un produit.
     */
    public String getCodeBarre() {
        return codeBarre;
    }

    /** Descriptif du produit. Peut être le résultat d'une accumulation de
     * descriptifs si le produit est composé
     */
    public String getDescriptif() {
        return descriptif;
    }

    /** Fournit le prix du produit.
     * Peut être calculé.
     */
    public float getPrix() {
        return prix;
    }

    /** Getter for property longueur.
     * @return Value of property longueur.
     */
    public float getLongueur() {
        return this.longueur;
    }

    /** Setter for property longueur.
     * @param longueur New value of property longueur.
     */
    public void setLongueur(float longueur) {
        this.longueur = longueur;
    }

    private float poids = 0;
    private float prix = 0;
    private String codeBarre;
    private String descriptif;

    /** Holds value of property longueur. */
    private float longueur;

}

public class Poids implements Produit {

    /** Creates a new instance of Poids */
    public Poids() {
    }

    public float getPoids() {
        return poids;
    }

    /** Code barre unique d'un produit.
     */
    public String getCodeBarre() {
        return codeBarre;
    }

    /** Descriptif du produit. Peut être le résultat d'une accumulation de
     * descriptifs si le produit est composé
     */
    public String getDescriptif() {
        return descriptif;
    }

    /** Fournit le prix du produit.
     * Peut être calculé.
     */
    public float getPrix() {
        return prix;
    }

    private float poids = 0;
    private float prix  = 0;
    private String codeBarre;
    private String descriptif;
}

public class ProduitException extends RuntimeException {
    public ProduitException() {
        super();
    }
    public ProduitException(String msg) {
        super(msg);
    }
    public ProduitException(Exception e) {
        super(e);
    }
}

public class ProduitComposite implements Produit {

    /** Creates a new instance of ProduitComposite */
    public ProduitComposite() {
        children = new ArrayList();
    }

    /** Ajoute un produit à la liste des composants
     * @param produit le produit que l'on veux ajouter au composite
     * @throws ProduitException Si le produit est null.
     */
    public void add(Produit produit) throws ProduitException {
        assert null != children;
        if (null == produit) {
            throw new ProduitException("Impossible d'ajouter un produit null");
        }
        children.add(produit);
    }

    /** Enlève un produit de la composition.
     * @param produit le produit à retirer de la composition.
     * @throws ProduitException Si le produit est null ou n'est pas dans la liste.
     */
    public void remove(Produit produit) throws ProduitException {
        assert null != children;
        if (null == produit) {
            throw new ProduitException("Impossible d'enlever un produit null");
        }

        if ( ! children.contains(produit)) {
            throw new ProduitException("Impossible d'enlever le produit, il n'est pas dans la liste");
        }

        children.remove(produit);
    }

    /** Renvoie la liste des composantes du produit sous la forme d'un itérateur.<p>
     * Voir le pattern itérateur.
     * @return La liste des composantes.
     */
    public Iterator getChildren() {
        assert null != children;
        return children.iterator();
    }

    /** Code barre unique d'un produit.
     * @return  le code barre du produit
     */
    public String getCodeBarre() {
        return codeBarre;
    }

    /** Descriptif du produit. Peut être le résultat d'une accumulation de
     * descriptifs si le produit est composé
     * @return  le descriptif composé
     */
    public String getDescriptif() {
        assert null != children;

        StringBuffer result = new StringBuffer();
        result.append(descriptif);
        result.append(" : (");

        for (Iterator i = children.iterator(); i.hasNext(); ) {
            Object objet = i.next();

            assert null != objet : "Un objet null a été trouvé dans la liste des composantes";
            assert objet instanceof Produit : "Un \"non produit\" a été trouvé dans la liste des composantes";

            Produit composant = (Produit)objet;

            result.append(composant.getDescriptif());
            if (i.hasNext()) { // on ajoute une virgule pour séparer les descriptifs
                result.append(", ");
            }
        }

        result.append(" )");
        return result.toString();
    }

    /** Fournit le prix du produit.
     * Peut être calculé.
     * @return  le prix calculé
     */
    public float getPrix() {
        float result = 0;
        for (Iterator i = children.iterator(); i.hasNext(); ) {
            Object objet = i.next();

            assert null != objet : "Un objet null a été trouvé dans la liste des composantes";
            assert objet instanceof Produit : "Un \"non produit\" a été trouvé dans la liste des composantes";

            Produit composant = (Produit)objet;

            result += composant.getPrix();
        }
        result = result * 0.9f; // soit une réducion de 10%
        return result;
    }

    private Collection children;
    private String codeBarre;
    private String descriptif;

}

Barre maBarre = new Barre();
maBarre.setPrix(25f);
maBarre.setDescriptif("Barre d'haltérophilie");
maBarre.setCodeBarre("BA0001");
maBarre.setLongueur(150f);

Poids leger = new Poids();
leger.setPrix(15f);
leger.setDescriptif("Poids d'haltère");
leger.setCodeBarre("PA0001");
leger.setPoids(0.5f);

Poids moyen = new Poids();
moyen.setPrix(17f);
moyen.setDescriptif("Poids d'haltère");
moyen.setCodeBarre("PA0002");
moyen.setPoids(1f);

Poids lourd = new Poids();
lourd.setPrix(19f);
lourd.setDescriptif("Poids d'haltère");
lourd.setCodeBarre("PA0003");
lourd.setPoids(1.5f);

ProduitComposite haltere = new ProduitComposite();
haltere.add(maBarre);
haltere.add(leger);
haltere.add(moyen);
haltere.add(lourd);

# Quizz

Et maintenant, un quizz pour voir si vous avez suivi !

?[What is the answer to Life, the Universe and Everything?]
-[ ] There is no answer to that!
-[ ] Sleep and eat
-[x] Easy, this is 42
-[ ] Peace & Love

?[What is the answer to Life, the Universe and Everything?]
-[ ] There is no answer to that!
-[ ] Sleep and eat
-[x] Easy, this is 42
-[ ] Peace & Love

?[What is the answer to Life, the Universe and Everything?]
-[ ] There is no answer to that!
-[ ] Sleep and eat
-[x] Easy, this is 42
-[ ] Peace & Love

?[What is the answer to Life, the Universe and Everything?]
-[ ] There is no answer to that!
-[ ] Sleep and eat
-[x] Easy, this is 42
-[ ] Peace & Love

?[What is the answer to Life, the Universe and Everything?]
-[ ] There is no answer to that!
-[ ] Sleep and eat
-[x] Easy, this is 42
-[ ] Peace & Love
