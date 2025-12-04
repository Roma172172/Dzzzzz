using System;
using System.Collections.Generic;

// Модель Product с использованием record (C# 9.0+)
public record Product(int Id, string Name, decimal Price)
{
    public override string ToString()
    {
        return $"Product {{ Id = {Id}, Name = {Name}, Price = {Price:F2} }}";
    }
}

// Класс Inventory для управления товарами
public class Inventory
{
    private readonly List<Product> _products = new List<Product>();

    // Добавление товара
    public void AddProduct(Product product)
    {
        _products.Add(product);
        Console.WriteLine($"Добавлен товар: {product}");
    }

    // Поиск товара по ID
    public Product FindProductById(int id)
    {
        return _products.Find(p => p.Id == id);
    }

    // Получение всех товаров (для демонстрации)
    public IEnumerable<Product> GetAllProducts()
    {
        return _products;
    }
}

class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine("--- Управление инвентарем ---\n");

        // Создаем инвентарь
        Inventory inventory = new Inventory();

        // Добавляем товары
        inventory.AddProduct(new Product(1, "Молоко", 80.50m));
        inventory.AddProduct(new Product(2, "Хлеб", 40.00m));
        inventory.AddProduct(new Product(3, "Сыр", 450.99m));

        Console.WriteLine("\n--- Поиск товара с ID 2 ---");
        Product foundProduct = inventory.FindProductById(2);
        if (foundProduct != null)
        {
            Console.WriteLine($"Найден товар: {foundProduct}");
        }
        else
        {
            Console.WriteLine("Товар с ID 2 не найден.");
        }

        Console.WriteLine("\n--- Поиск товара с ID 99 ---");
        Product notFoundProduct = inventory.FindProductById(99);
        if (notFoundProduct != null)
        {
            Console.WriteLine($"Найден товар: {notFoundProduct}");
        }
        else
        {
            Console.WriteLine("Товар с ID 99 не найден.");
        }
    }
}
