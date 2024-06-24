![image](https://github.com/ArtworkPunk/TEST1/assets/67797794/e4d62727-1be5-4939-831e-fb0e8b245910)

```
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Data.Common;
using System.Data.SqlClient;
using System.Drawing;
using System.Linq;
using System.Reflection;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
 
namespace test1
{
    public partial class Form1 : Form
    {
        SqlConnection connect;
        SqlDataAdapter adapter;
        SqlCommand cmd;
        DataTable dt;
        string path = "Data Source=(LocalDB)\\MSSQLLocalDB;AttachDbFilename=C:\\Users\\nikit\\Desktop\\code\\test1\\test1\\Database1.mdf;Integrated Security=True";
        string quary = "SELECT * FROM [dbo].[Table]";
        SqlCommandBuilder builder;
        public Form1()
        {
            InitializeComponent();
        }
 
        private void открытьToolStripMenuItem_Click(object sender, EventArgs e)
        {
            connect = new SqlConnection(path);
            cmd = new SqlCommand(quary, connect);
            adapter = new SqlDataAdapter(cmd);
            dt = new DataTable();
            try
            {
                connect.Open();
                adapter.Fill(dt);
                dataGridView1.DataSource = dt;
                connect.Close();
            }
            catch (Exception ex) {
                MessageBox.Show(ex.Message);
                connect.Close();
            }
        }
 
        private void toolStripButton1_Click(object sender, EventArgs e)
        {
            connect = new SqlConnection(path);
            cmd = new SqlCommand(quary, connect);
            adapter = new SqlDataAdapter(cmd);
            dataGridView1.DataSource = dt;
            builder = new SqlCommandBuilder(adapter);
            adapter.UpdateCommand = builder.GetUpdateCommand();
            adapter.InsertCommand = builder.GetInsertCommand();
            adapter.DeleteCommand = builder.GetDeleteCommand();
            try
            {
                connect.Open();
                adapter.Update(dt);
                connect.Close();
            }
            catch (Exception ex)
            {
                MessageBox.Show(ex.Message);
                connect.Close();
            }
        }
    }
```
