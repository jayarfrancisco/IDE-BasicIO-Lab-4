public class Main {
    // Node class for Doubly Linked List
    static class Node {
        int data;
        Node prev, next;

        Node(int data) {
            this.data = data;
            this.prev = null;
            this.next = null;
        }
    }

    // Doubly Linked List class
    static class DoublyLinkedList {
        private Node head, tail;
        private int size;

        // Add at the beginning
        public void addFirst(int data) {
            Node newNode = new Node(data);
            if (head == null) {
                head = tail = newNode;
            } else {
                newNode.next = head;
                head.prev = newNode;
                head = newNode;
            }
            size++;
        }

        // Add at the end
        public void addLast(int data) {
            Node newNode = new Node(data);
            if (tail == null) {
                head = tail = newNode;
            } else {
                tail.next = newNode;
                newNode.prev = tail;
                tail = newNode;
            }
            size++;
        }

        // Remove from the beginning
        public void removeFirst() {
            if (head == null) {
                System.out.println("List is empty!");
                return;
            }
            if (head == tail) {
                head = tail = null;
            } else {
                head = head.next;
                head.prev = null;
            }
            size--;
        }

        // Remove from the end
        public void removeLast() {
            if (tail == null) {
                System.out.println("List is empty!");
                return;
            }
            if (head == tail) {
                head = tail = null;
            } else {
                tail = tail.prev;
                tail.next = null;
            }
            size--;
        }

        // Get data at index
        public int get(int index) {
            if (index < 0 || index >= size) {
                System.out.println("Index out of bounds!");
                return -1;
            }
            Node current = head;
            for (int i = 0; i < index; i++) {
                current = current.next;
            }
            return current.data;
        }

        // Search for data
        public boolean contains(int data) {
            Node current = head;
            while (current != null) {
                if (current.data == data) return true;
                current = current.next;
            }
            return false;
        }

        // Show list forward
        public void display() {
            Node current = head;
            while (current != null) {
                System.out.print(current.data + " ");
                current = current.next;
            }
            System.out.println();
        }

        // Reverse the list
        public void reverse() {
            Node current = head;
            Node temp = null;

            while (current != null) {
                temp = current.prev;
                current.prev = current.next;
                current.next = temp;
                current = current.prev;
            }

            if (temp != null) {
                head = temp.prev;
            }
        }

        // Swap two nodes by index (beginner version: swap data only)
        public void swapNodes(int index1, int index2) {
            if (index1 == index2) return;
            if (index1 < 0 || index1 >= size || index2 < 0 || index2 >= size) {
                System.out.println("Index out of bounds!");
                return;
            }

            Node node1 = head;
            Node node2 = head;

            for (int i = 0; i < index1; i++) node1 = node1.next;
            for (int i = 0; i < index2; i++) node2 = node2.next;

            int temp = node1.data;
            node1.data = node2.data;
            node2.data = temp;
        }

        public int size() {
            return size;
        }
    }

    // Main method for testing
    public static void main(String[] args) {
        DoublyLinkedList list = new DoublyLinkedList();

        list.addFirst(10);
        list.addLast(20);
        list.addLast(30);
        list.addLast(40);

        System.out.print("List: ");
        list.display();

        list.removeFirst();
        System.out.print("After removing first: ");
        list.display();

        list.removeLast();
        System.out.print("After removing last: ");
        list.display();

        System.out.println("Get index 1: " + list.get(1));
        System.out.println("Contains 20? " + list.contains(20));

        list.reverse();
        System.out.print("Reversed list: ");
        list.display();

        list.swapNodes(0, 1);
        System.out.print("After swapping index 0 and 1: ");
        list.display();
    }
}
