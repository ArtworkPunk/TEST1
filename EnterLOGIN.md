![image](https://github.com/ArtworkPunk/TEST1/assets/67797794/da835bed-e442-478d-9478-95d83b992d16)
```
using System;
 
using System.Data.SqlClient;
using System.Windows.Forms;
 
namespace Database
{
    public partial class Form1 : Form
    {
        string path = "Data Source=(LocalDB)\\MSSQLLocalDB;AttachDbFilename=C:\\Users\\nikit\\Desktop\\code\\Database\\Database\\Database1.mdf;Integrated Security=True";
        SqlConnection connect;
        SqlCommand cmd;
        string quary = "SELECT * FROM [dbo].[Table] WHERE Login = @Login AND Password = @Password";
        string inputreg = "INSERT INTO [dbo].[Table] (Login,Password) VALUES (@Login,@Password)";
        public Form1()
        {
            InitializeComponent();
        }

        private void Login_Click(object sender, EventArgs e)
        {
            string Login = textBox1.Text;
            string Password = textBox2.Text;
            connect = new SqlConnection(path);
            cmd = new SqlCommand(quary,connect);
            try
            {
                connect.Open();
                cmd.Parameters.AddWithValue("@Login", Login);
                cmd.Parameters.AddWithValue("@Password", Password);
                int count = (int)cmd.ExecuteScalar();
                if (count > 0) {
                    MessageBox.Show($"Вы вошли под {Login}");
                    this.Hide();
                    Form2 form2 = new Form2();
                    form2.Show();
                    connect.Close();
                }
            }
            catch (Exception sex) {
                MessageBox.Show(sex.Message,"Ошибка доступа",MessageBoxButtons.OK,MessageBoxIcon.Error);
                connect.Close();
            }
        }
 
        private void Register_Click(object sender, EventArgs e)
        {
            string Login = textBox1.Text;
            string Password = textBox2.Text;
            connect = new SqlConnection(path);
            cmd = new SqlCommand(inputreg, connect);
            try
            {
                connect.Open();
                cmd.Parameters.AddWithValue("@Login", Login);
                cmd.Parameters.AddWithValue("@Password", Password);
                if (Login.Length == 0)
                {
                    MessageBox.Show("Вы не заполнили данные");
                    connect.Close();
 
                }
                else if (Password.Length < 10)
                {
                    MessageBox.Show("Пароль должен быть больше 10 символов");
                    connect.Close();
                }
                else {
                    cmd.ExecuteNonQuery();
                    MessageBox.Show("Регистрация пользователя прошла успешно");
                    connect.Close();
                }
            }
            catch (Exception sex) {
                MessageBox.Show(sex.Message);
                connect.Close();
            }
        }
    }
}
```
