# Factory Method (Fabrika Metodu)

Factory Method, **creational (oluşturucu) design pattern** kategorisine girer.

## 🧠 Amaç

Nesne oluşturma (object creation) sorumluluğunu alt sınıflara devretmektir.

Üst sınıf, hangi somut sınıfın üretildiğini bilmez.

---

## 🧩 Yapı

- **Product (Ürün):** Ortak arayüz → `ITasiyici`
- **Concrete Product:** `Kamyon`, `Gemi`
- **Creator (Fabrika):** `Lojistik`
- **Concrete Creator:** `KaraLojistik`, `DenizLojistik`

---
<h1>UML Diyagramı</h1>
<img width="1024" height="559" alt="image" src="https://github.com/user-attachments/assets/92a665fb-916b-4f1f-9ecf-21867ef100ab" />
---

## 💻 Örnek Kod (C#)

```csharp
// Tüm taşıma araçlarının ortak arayüzü
public interface ITasiyici
{
    void TeslimEt();
}

// Concrete Product
public class Kamyon : ITasiyici
{
    public void TeslimEt()
    {
        Console.WriteLine("Karayolu ile paket teslim edildi.");
    }
}

// Concrete Product
public class Gemi : ITasiyici
{
    public void TeslimEt()
    {
        Console.WriteLine("Deniz yolu ile paket teslim edildi.");
    }
}

// Creator (Fabrika)
public abstract class Lojistik
{
    public abstract ITasiyici TasimaOlustur();

    public void OperasyonuBaslat()
    {
        ITasiyici tasiyici = TasimaOlustur();
        tasiyici.TeslimEt();
    }
}

// Concrete Creator
public class KaraLojistik : Lojistik
{
    public override ITasiyici TasimaOlustur() => new Kamyon();
}

// Concrete Creator
public class DenizLojistik : Lojistik
{
    public override ITasiyici TasimaOlustur() => new Gemi();
}

// Client
class Program
{
    static void Main()
    {
        Lojistik lojistik = new KaraLojistik();
        lojistik.OperasyonuBaslat(); 
        // Output: Karayolu ile paket teslim edildi.
    }
}

```
<h2>Çıktı</h2>
<img width="388" height="71" alt="image" src="https://github.com/user-attachments/assets/a60dc569-c133-4940-85ba-6cc323473c95" />

<h1>Örnek-2 </h1>
<img width="830" height="780" alt="image" src="https://github.com/user-attachments/assets/33c40383-605a-4b28-ad1d-5435f2f6ea2e" />

## 💻 Örnek Kod (C#)

```csharp
//1. Adım Sözleşme
public interface IEnemies
{
    string Name { get; }
    int Health { get; }
    void Attack();
}
public class Goblin : IEnemies
{
    public string Name { get; private set; }
    public int Health { get; private set; }
    public Goblin()
    {
        Name = "Goblin";
        Health = 50;
    }
    public void Attack()
    {
        Console.WriteLine($"{Name} , Can: {Health}");
    }
   
}
public class Dragon : IEnemies
{
    public string Name { get; private set; }
    public int Health { get; private set; }
    public Dragon()
    {
        Name = "Dragon";
        Health = 150;
    }
    public void Attack()
    {
        Console.WriteLine($"{Name} ateş püskürttü , kalan can : {Health}");
    }
}
public class Orc : IEnemies
{
    public string Name { get; private set; }
    public int Health { get; private set; }
    public Orc()
    {
        Name = "Orc";
        Health = 400;
    }
    public void Attack()
    {
        Console.WriteLine($"{Name} , Can : {Health}");
    }
}
// Ana soyut fabrika şeması
public abstract class EnemyFactory
{
    // Bu metot çağrıldığında geriye kurallara uyan (IEnemies) bir düşman dönecek
    public abstract IEnemies CreateEnemy();
}

// Goblin Üreten Fabrika
public class GoblinFactory : EnemyFactory
{
    public override IEnemies CreateEnemy() => new Goblin();
}

// Orc Üreten Fabrika
public class OrcFactory : EnemyFactory
{
    public override IEnemies CreateEnemy() => new Orc();
}

// Dragon Üreten Fabrika
public class DragonFactory : EnemyFactory
{
    public override IEnemies CreateEnemy() => new Dragon();
}

class Program
{
    public static void Main()
    {
        EnemyFactory fabrika = new DragonFactory(); // Boss odasına geldik!

        // Fabrikayı çalıştırıyoruz. Arka planda 'new Dragon()' dönüyor 
        // ama Main metodu bunu görmüyor, sadece 'IEnemies' tipinde bir düşman alıyor.
        IEnemies canavar = fabrika.CreateEnemy();

        // Düşman kimse ona göre saldırıyor
        canavar.Attack(); // Çıktı: Dragon ateş püskürttü!


    }
}
```
## Çıktı
<img width="381" height="73" alt="image" src="https://github.com/user-attachments/assets/6092a9c5-26eb-42c0-8dec-16ef2a854f91" />
