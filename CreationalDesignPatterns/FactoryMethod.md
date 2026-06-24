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

