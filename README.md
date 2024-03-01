1. Используя команду cat в терминале операционной системы Linux, создать
два файла Домашние животные (заполнив файл собаками, кошками,
хомяками) и Вьючные животными заполнив файл Лошадьми, верблюдами и
ослы), а затем объединить их. Просмотреть содержимое созданного файла.
Переименовать файл, дав ему новое имя (Друзья человека).

![image](https://github.com/dafeo1991/itog_work/assets/118327697/ff0198f0-763a-438f-9982-85940c91a10f)

2. Создать директорию, переместить файл туда.

![image](https://github.com/dafeo1991/itog_work/assets/118327697/f033f89f-1062-4d5f-8316-ae1c02ac2934)

3. Подключить дополнительный репозиторий MySQL. Установить любой пакет
из этого репозитория.

![image](https://github.com/dafeo1991/itog_work/assets/118327697/36432c2c-6632-4f06-a00b-bcdbf34b488f)

4. Установить и удалить deb-пакет с помощью dpkg

![image](https://github.com/dafeo1991/itog_work/assets/118327697/4f714995-f8b7-4ea7-bd6c-2eb249ce2e86)

5. Выложить историю команд в терминале ubuntu

![image](https://github.com/dafeo1991/itog_work/assets/118327697/0072e707-55d6-4dd7-9d51-14e856f4ecd4)

6. Нарисовать диаграмму, в которой есть класс родительский класс, домашние
животные и вьючные животные, в составы которых в случае домашних
животных войдут классы: собаки, кошки, хомяки, а в класс вьючные животные
войдут: Лошади, верблюды и ослы).

![image](https://github.com/dafeo1991/itog_work/assets/118327697/63846b3d-76ab-410b-b3f4-72a6fc604a45)


7. В подключенном MySQL репозитории создать базу данных “Друзья
человека”

![image](https://github.com/dafeo1991/itog_work/assets/118327697/7f460ca7-63c9-4b2c-8223-5409bed6925e)


8. Создать таблицы с иерархией из диаграммы в БД

 ![image](https://github.com/dafeo1991/itog_work/assets/118327697/5b7854b3-64c1-4530-b1d7-8cad4ec1e12e)

9. Заполнить низкоуровневые таблицы именами(животных), командами которые они выполняют и датами рождения

 ![image](https://github.com/dafeo1991/itog_work/assets/118327697/57ec86af-7e36-4de3-a7cd-ef1a6e77c7eb)

 10. Удалив из таблицы верблюдов, т.к. верблюдов решили перевезти в другой
питомник на зимовку. Объединить таблицы лошади, и ослы в одну таблицу.

![image](https://github.com/dafeo1991/itog_work/assets/118327697/66c5a83a-f2f4-454b-86b5-990535372fc1)

11.Создать новую таблицу “молодые животные” в которую попадут все
животные старше 1 года, но младше 3 лет и в отдельном столбце с точностью
до месяца подсчитать возраст животных в новой таблице

![image](https://github.com/dafeo1991/itog_work/assets/118327697/ba77d263-c67a-4d68-b102-046ede10dc0c)

![image](https://github.com/dafeo1991/itog_work/assets/118327697/1680b52c-4a0f-43e5-81c6-96b26eddd41a)

12. Объединить все таблицы в одну, при этом сохраняя поля, указывающие на
прошлую принадлежность к старым таблицам.

![image](https://github.com/dafeo1991/itog_work/assets/118327697/260b6976-e26b-4b37-b752-d0cc5b932899)

13.Создать класс с Инкапсуляцией методов и наследованием по диаграмме.
14. Написать программу, имитирующую работу реестра домашних животных.
В программе должен быть реализован следующий функционал:
14.1 Завести новое животное
14.2 определять животное в правильный класс
14.3 увидеть список команд, которое выполняет животное
14.4 обучить животное новым командам
14.5 Реализовать навигацию по меню
15.Создайте класс Счетчик, у которого есть метод add(), увеличивающий̆
значение внутренней̆int переменной̆на 1 при нажатие “Завести новое
животное” Сделайте так, чтобы с объектом такого типа можно было работать в
блоке try-with-resources. Нужно бросить исключение, если работа с объектом
типа счетчик была не в ресурсном try и/или ресурс остался открыт. Значение
считать в ресурсе try, если при заведения животного заполнены все поля

import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

abstract class Animal {
    private String name;
    private List<String> commands = new ArrayList<>();

    public Animal(String name) {
        this.name = name;
    }

    public void addCommand(String command) {
        commands.add(command);
    }

    public String getName() {
        return name;
    }

    public List<String> getCommands() {
        return commands;
    }
}

class Cat extends Animal {
    public Cat(String name) {
        super(name);
    }
}

class Counter implements AutoCloseable {
    private int count;

    public void add() {
        count++;
    }

    public int getCount() {
        return count;
    }

    @Override
    public void close() throws Exception {
        if (count == 0) {
            throw new Exception("Счетчик не использовался.");
        }
        
    }
}

class Dog extends Animal {
    public Dog(String name) {
        super(name);
    }
}

class Hamster extends Animal {
    public Hamster(String name) {
        super(name);
    }
}

public class Main {
    public static void main(String[] args) {
        PetRegistry registry = new PetRegistry();
        boolean exit = false;
        Scanner scanner = new Scanner(System.in);

        try (Counter counter = new Counter()) {
            while (!exit) {
                registry.showMenu();
                int choice = scanner.nextInt();
                scanner.nextLine(); // Игнорируем перевод строки после числа

                switch (choice) {
                    case 1:
                        registry.registerPet(counter);
                        break;
                    case 2:
                        registry.listCommands();
                        break;
                    case 3:
                        registry.teachCommand();
                        break;
                    case 4:
                        exit = true;
                        break;
                    default:
                        System.out.println("Неверный выбор, попробуйте снова.");
                }
            }
        } catch (Exception e) {
            System.out.println("Произошла ошибка: " + e.getMessage());
        }
    }
}

class Mouse extends Animal {
    public Mouse(String name) {
        super(name);
    }
}

import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

class PetRegistry {
    private List<Animal> pets = new ArrayList<>();
    private Scanner scanner = new Scanner(System.in);

    public void registerPet(Counter counter) {
        System.out.print("Введите тип животного (Dog/Cat/Hamster/Mouse): ");
        String type = scanner.nextLine();
        System.out.print("Введите имя животного: ");
        String name = scanner.nextLine();

        Animal pet = null;
        if ("Dog".equalsIgnoreCase(type)) {
            pet = new Dog(name);
        } else if ("Cat".equalsIgnoreCase(type)) {
            pet = new Cat(name);
        } else if ("Hamster".equalsIgnoreCase(type)){
            pet = new Hamster(name);
        } else if ("Mouse".equalsIgnoreCase(type)){
            pet = new Mouse(name);
        }
        if (pet != null) {
            pets.add(pet);
            counter.add();
            System.out.println("Животное " + pet.getName() + " добавлено.");
        } else {
            System.out.println("Неизвестный тип животного.");
        }
    }

    public void listCommands() {
        System.out.print("Введите имя животного: ");
        String name = scanner.nextLine();
        for (Animal pet : pets) {
            if (pet.getName().equalsIgnoreCase(name)) {
                System.out.println("Команды для " + pet.getName() + ": " + pet.getCommands());
                return;
            }
        }
        System.out.println("Животное не найдено.");
    }

    public void teachCommand() {
        System.out.print("Введите имя животного: ");
        String name = scanner.nextLine();
        System.out.print("Введите команду для обучения: ");
        String command = scanner.nextLine();
        for (Animal pet : pets) {
            if (pet.getName().equalsIgnoreCase(name)) {
                pet.addCommand(command);
                System.out.println("Животное " + pet.getName() + " обучено команде: " + command);
                return;
            }
        }
        System.out.println("Животное не найдено.");
    }

    public void showMenu() {
        System.out.println("   Выберите пункт из меню:");
        System.out.println("1. Завести новое животное");
        System.out.println("2. Показать список команд животного");
        System.out.println("3. Обучить животное новой команде");
        System.out.println("4. Выйти");
    }
}
