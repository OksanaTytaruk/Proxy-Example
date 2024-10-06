# Proxy Example

Цей репозиторій містить приклад патерну проектування "Замісник".

## Патерн Замісник (Proxy)

Патерн "Замісник" використовується для заміщення реальних об'єктів і контролю доступу до них.

### Приклад коду:

```csharp
// Інтерфейс для реального об'єкта
public interface IImage
{
    void Display();
}

// Реальний об'єкт
public class RealImage : IImage
{
    private string _fileName;

    public RealImage(string fileName)
    {
        _fileName = fileName;
        LoadFromDisk();
    }

    private void LoadFromDisk()
    {
        Console.WriteLine($"Loading {_fileName}");
    }

    public void Display()
    {
        Console.WriteLine($"Displaying {_fileName}");
    }
}

// Замісник
public class ProxyImage : IImage
{
    private RealImage _realImage;
    private string _fileName;

    public ProxyImage(string fileName)
    {
        _fileName = fileName;
    }

    public void Display()
    {
        if (_realImage == null)
        {
            _realImage = new RealImage(_fileName);
        }
        _realImage.Display();
    }
}

// Клієнтський код
class Program
{
    static void Main(string[] args)
    {
        IImage image1 = new ProxyImage("photo1.jpg");
        IImage image2 = new ProxyImage("photo2.jpg");

        // Зображення завантажується з диску тільки при першому виклику
        image1.Display();
        image1.Display();

        // Зображення завантажується з диску тільки при першому виклику
        image2.Display();
        image2.Display();
    }
}
