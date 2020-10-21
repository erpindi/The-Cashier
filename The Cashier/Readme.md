# The Cashier
Aplikasi Ini Berfungsi Untuk Menghitung Jumlah Harga Barang Yang Telah Dibeli

### Fungsionalitas
* User Dapat Menghitung Harga Barang yang dibeli dengan otomatis
* User Dapat Menambahkan Barang yang telah dibeli

### Penjelasan Code
Diawali dari MainWindow.xaml.cs dengan source code sebagai berikut :


public MainWindow()

        {
            InitializeComponent();
            calculator = new Calculator();
            listBox.ItemsSource = calculator.getListItem();
        }

        private void AddButton_Click(object sender, RoutedEventArgs e)
        {
            string title = itemNameBox.Text;
            int quantity = int.Parse(quantityBox.Text);
            string type = typeBox.Text;
            double price = double.Parse(priceBox.Text);

            Item item = new Item(new Random().Next(),title,quantity,price,price,type);
            calculator.addItem(item);
            double total = calculator.getTotal();

            totalLabel.Content = String.Format("Rp. {0}", total);

            listBox.Items.Refresh();

        }

Setelah itu di tambahkan class dengan nama Item.cs dengan source code sebagai berikut :

 public string getTitle()

        {
            return title;
        }
        public int getQuantity()
        {
            return quantity;
        }
        public string getType()
        {
            return type;
        }
        public double getPrice()
        {
            return price;
        }
        public double getSubTotal()
        {
            subtotal = price * quantity;
            return subtotal;
        }

Setelah ditambahkan Item.cs tambah lagi dengan nama calculator.cs sebagai penghitung harga dengan source code sebagai berikut :

class Calculator

    {
        private List<Item> listItem;
        private double total = 0;

        public Calculator()
        {
            this.listItem = new List<Item>();
        }
        public void addItem(Item item)
        {
            this.listItem.Add(item);
            this.total += item.getSubTotal();
        }
        public double getTotal()
        {
            return total;
        }
        public List<Item> getListItem()
        {
            return listItem;
        }
    }

Prinsip Single Responsibility dapat di temukan pada source code berikut :

public void addItem(Item item)

        {
            this.listItem.Add(item);
            this.total += item.getSubTotal();
        }
 Yang bertujuan untuk menambahkan item dan menghitung SubTotal 
