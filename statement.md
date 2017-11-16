import java.util.ArrayList;

interface Graphic {

    //Imprime le graphique.
    public void print();

}

class CompositeGraphic implements Graphic {

    //Collection de graphiques enfants.
    private ArrayList<Graphic> mChildGraphics = new ArrayList<Graphic>();

    //Imprime le graphique.
    public void print() {
        for (Graphic graphic : mChildGraphics) {
            graphic.print();
        }
    }

    //Ajoute le graphique à la composition.
    public void add(Graphic graphic) {
        mChildGraphics.add(graphic);
    }

    //Retire le graphique de la composition.
    public void remove(Graphic graphic) {
        mChildGraphics.remove(graphic);
    }

}

class Ellipse implements Graphic {

    //Imprime le graphique.
    public void print() {
        System.out.println("Ellipse");
    }

}

public class Program {

    public static void main(String[] args) {
        //Initialise quatre ellipses
        Ellipse ellipse1 = new Ellipse();
        Ellipse ellipse2 = new Ellipse();
        Ellipse ellipse3 = new Ellipse();
        Ellipse ellipse4 = new Ellipse();

        //Initialise trois graphiques composites
        CompositeGraphic graphic = new CompositeGraphic();
        CompositeGraphic graphic1 = new CompositeGraphic();
        CompositeGraphic graphic2 = new CompositeGraphic();

        //Composes les graphiques
        graphic1.add(ellipse1);
        graphic1.add(ellipse2);
        graphic1.add(ellipse3);

        graphic2.add(ellipse4);

        graphic.add(graphic1);
        graphic.add(graphic2);

        //Imprime le graphique complet (quatre fois la chaîne "Ellipse").
        graphic.print();
    }
}
