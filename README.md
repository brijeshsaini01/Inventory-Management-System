import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

public class test {
    public static void main(String[] args) {
        Inventory inventory = new Inventory();

        Product product1 = new Product(1, "Laptop", 999.99, 10);
        Product product2 = new Product(2, "Smartphone", 499.99, 20);
        Product product3 = new Product(3, "Tablet", 299.99, 15);

        inventory.addProduct(product1);
        inventory.addProduct(product2);
        inventory.addProduct(product3);

        Scanner scanner = new Scanner(System.in);

        while (true) {
            System.out.println("\nOptions:");
            System.out.println("1. Display Products");
            System.out.println("2. Update Product Quantity");
            System.out.println("3. Exit");
            System.out.print("Enter your choice: ");
            int choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    inventory.displayProducts();
                    break;
                case 2:
                    System.out.print("Enter the product ID: ");
                    int productId = scanner.nextInt();
                    System.out.print("Enter the new quantity: ");
                    int newQuantity = scanner.nextInt();
                    inventory.updateProductQuantity(productId, newQuantity);
                    System.out.println("Product quantity updated.");
                    break;
                case 3:
                    System.out.println("Exiting the system.");
                    System.exit(0);
                default:
                    System.out.println("Invalid choice. Please try again.");
            }
        }
    }

    static class Product {
        private int id;
        private String name;
        private double price;
        private int quantity;

        public Product(int id, String name, double price, int quantity) {
            this.id = id;
            this.name = name;
            this.price = price;
            this.quantity = quantity;
        }

        public int getId() {
            return id;
        }

        public String getName() {
            return name;
        }

        public double getPrice() {
            return price;
        }

        public int getQuantity() {
            return quantity;
        }
    }

    static class Inventory {
        private List<Product> products;

        public Inventory() {
            products = new ArrayList<>();
        }

        public void addProduct(Product product) {
            products.add(product);
        }

        public void displayProducts() {
            System.out.println("Product List:");
            for (Product product : products) {
                System.out.println("ID: " + product.getId() + ", Name: " + product.getName() + ", Price: $" + product.getPrice() + ", Quantity: " + product.getQuantity());
            }
        }

        public Product findProductById(int id) {
            for (Product product : products) {
                if (product.getId() == id) {
                    return product;
                }
            }
            return null;
        }

        public void updateProductQuantity(int id, int newQuantity) {
            Product product = findProductById(id);
            if (product != null) {
                product.quantity = newQuantity;
            }
        }
    }
}
