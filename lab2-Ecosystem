import java.util.Random;
import java.util.ArrayList;

abstract class Animal {
    public abstract String toString();
}

class Bear extends Animal {
    @Override
    public String toString() {
        return "B";
    }
}

class Fish extends Animal {
    @Override
    public String toString() {
        return "F";
    }
}

public class Ecosystem {
    private Animal[] river;
    private Random random;

    public Ecosystem(int riverSize) {
        this.river = new Animal[riverSize];
        this.random = new Random();
        for (int i = 0; i < river.length; i++) {
            int choice = random.nextInt(3);
            if (choice == 1) {
                river[i] = new Bear();
            } else if (choice == 2) {
                river[i] = new Fish();
            } else {
                river[i] = null;
            }
        }
    }

    public void runStep() {
        Animal[] newRiver = new Animal[river.length];
        for (int i = 0; i < river.length; i++) {
            if (river[i] != null) {
                int move = random.nextInt(3) - 1;
                int newPos = i + move;
                if (newPos < 0 || newPos >= river.length) {
                    newPos = i;
                }
                if (newRiver[newPos] == null) {
                    newRiver[newPos] = river[i];
                } else {
                    handleCollision(newRiver, newPos, river[i]);
                }
            }
        }
        river = newRiver;
    }

    private void handleCollision(Animal[] newRiver, int pos, Animal incoming) {
        Animal existing = newRiver[pos];
        if (existing.getClass() == incoming.getClass()) {
            placeNewAnimal(incoming);
        } else {
            if (existing instanceof Bear || incoming instanceof Bear) {
                newRiver[pos] = new Bear();
            }
        }
    }

    private void placeNewAnimal(Animal parent) {
        ArrayList<Integer> emptyCells = new ArrayList<>();
        for (int i = 0; i < river.length; i++) {
            if (river[i] == null) emptyCells.add(i);
        }
        if (!emptyCells.isEmpty()) {
            int idx = emptyCells.get(random.nextInt(emptyCells.size()));
            if (parent instanceof Bear) {
                river[idx] = new Bear();
            } else if (parent instanceof Fish) {
                river[idx] = new Fish();
            }
        }
    }

    public void visualize() {
        for (Animal animal : river) {
            System.out.print(animal == null ? "-" : animal.toString());
            System.out.print(" ");
        }
        System.out.println();
    }

    public static void main(String[] args) {
        Ecosystem eco = new Ecosystem(20);
        eco.visualize();
        for (int step = 0; step < 10; step++) {
            eco.runStep();
            eco.visualize();
        }
    }
}
