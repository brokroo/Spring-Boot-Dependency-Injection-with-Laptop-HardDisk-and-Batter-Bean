# Spring Boot – Dependency Injection with Laptop, HardDisk and Batter Beans

This simple Spring Boot project demonstrates **Dependency Injection (DI)** and **`@Autowired`** using three bean classes:

- `Laptop`
- `HardDisk`
- `Batter` (Battery)

The beans are wired together using Spring’s IoC container.

---

## Project Overview

All classes are defined in a **single file**: `DemoApplication.java`.

```java
@SpringBootApplication
public class DemoApplication {

    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }

    @Bean
    public CommandLineRunner runner(Laptop laptop) {
        return args -> laptop.start();
    }

    @Component
    public static class Laptop {

        private final HardDisk hardDisk;
        private final Batter batter;

        @Autowired
        public Laptop(HardDisk hardDisk, Batter batter) {
            this.hardDisk = hardDisk;
            this.batter = batter;
        }

        public void start() {
            System.out.println("Laptop starting...");
            hardDisk.readData();
            batter.supplyPower();
            System.out.println("Laptop started successfully.");
        }
    }

    @Component
    public static class HardDisk {
        public void readData() {
            System.out.println("HardDisk: Reading data...");
        }
    }

    @Component
    public static class Batter {
        public void supplyPower() {
            System.out.println("Batter: Supplying power to laptop...");
        }
    }
}
