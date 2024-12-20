![image](https://github.com/user-attachments/assets/6b7e487e-d80b-4213-8dde-86acda6f6fae)

![image](https://github.com/user-attachments/assets/b74b9db9-303c-4221-98e1-6f8ae3c85652)

@Transactional

The @Transactional annotation in the OrderService class is used to manage database transactions declaratively in a Spring application. If a method in the OrderService performs multiple database operations (e.g., creating an order, updating inventory, and recording a payment), @Transactional ensures that these operations are treated as a single transaction. If any operation fails, all changes are rolled back.




