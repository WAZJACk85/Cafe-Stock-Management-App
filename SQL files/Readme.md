This folder holds the SQL Files from the project and I have noted the Queries I have used in the creation of the tables below.

![image](https://user-images.githubusercontent.com/20317523/138116737-c5023d15-d1cd-4f45-875d-03adf168310c.png)


As you can also see in the image Above, I have created a basic items dbo table, and this is connected to my app in such a way that the application when information is inputted and sent, via a click will add, remove, update and place orders to be summed and totalled (then printed in pdf).

SQL Query Code so far in the project:-

create database Cafe4

create table items(
iid int identity(1,1) primary key,
name varchar(250)not null,
category varchar(250) not null,
price bigint not null
);



See SQL and C# code for adding items into my internal SQL Database below:- 

I will append another folder, to this project in the next few weeks, showing a network 'live' database connection and code, as an alternative displaying a live setup.

ADD ITEMS to DB

using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
using Microsoft.VisualBasic.PowerPacks;

namespace Cafe_Menu4.AllUserControls
{
    public partial class UC_AddItems : UserControl
    {
        function fn = new function();
        String query;
        public UC_AddItems()
        {
            InitializeComponent();
        }

       

        private void btnAddItem_Click(object sender, EventArgs e)
        {
            query = "insert into items (name,category,price) values ('"+txtItem.Text+"','"+txtCategory.Text+"',"+txtPrice.Text+")";
            fn.setData(query);
            clearAll();
        }

    public void clearAll()
        {
            txtCategory.SelectedIndex = -1;
            txtItem.Clear();
            txtPrice.Clear();
        }

        private void UC_AddItems_Leave(object sender, EventArgs e)
        {
            clearAll();
        }
    }
}


Here is the code for updating items:-

UPDATE ITEMS ON DB

using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace Cafe_Menu4.AllUserControls
{
    public partial class UC_UpdateItems : UserControl
    {
        function fn = new function();
        String query;
        public UC_UpdateItems()
        {
            InitializeComponent();
        }

        private void UC_UpdateItems_Load(object sender, EventArgs e)
        {
            loadData();
        }
        public void loadData()
        {
            query = "select * from items";
            DataSet ds = fn.getData(query);
            guna2DataGridView1.DataSource = ds.Tables[0];
        }

        private void txtSearchItem_TextChanged(object sender, EventArgs e)
        {
            query = "select *from items where name like '" + txtSearchItem.Text + "%'";
            DataSet ds = fn.getData(query);
            guna2DataGridView1.DataSource = ds.Tables[0];   
        }

        int id;
        private void guna2DataGridView1_CellClick(object sender, DataGridViewCellEventArgs e)
        {
            id = int.Parse(guna2DataGridView1.Rows[e.RowIndex].Cells[0].Value.ToString());
            String category = guna2DataGridView1.Rows[e.RowIndex].Cells[2].Value.ToString();
            String name = guna2DataGridView1.Rows[e.RowIndex].Cells[1].Value.ToString();
            int price = int.Parse(guna2DataGridView1.Rows[e.RowIndex].Cells[3].Value.ToString());

            txtCategory.Text = category;
            txtName.Text = name;
            txtPrice.Text = price.ToString();
        }

        private void btnUpdate_Click(object sender, EventArgs e)
        {
            query = "update items set name= '" + txtName.Text + "',category = '" + txtCategory.Text + "',price=" + txtPrice.Text + "where iid = " + id + "";
            fn.setData(query);
            loadData();

            txtName.Clear();
            txtCategory.Clear();
            txtPrice.Clear();
        }
    }
}


Function c# file for SQL connection functions (and dataset functions):-

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Data.SqlClient;
using System.Data;
using System.Windows.Forms;

namespace Cafe_Menu4
{
    class function
    {
        protected SqlConnection GetConnection()
        {
            SqlConnection con = new SqlConnection();
            con.ConnectionString = "data source =LAPTOP-LL7MF4G0\\MSSQL_APPOINT;database = Cafe4; Integrated security =True";
            return con;

        }
        public DataSet getData(String query)
        {
            SqlConnection con = GetConnection();
            SqlCommand cmd = new SqlCommand();
            cmd.Connection = con;
            cmd.CommandText = query;
            SqlDataAdapter da = new SqlDataAdapter(cmd);
            DataSet ds = new DataSet();
            da.Fill(ds);
            return ds;
        }

        public void setData(String query)
        {
            SqlConnection con = GetConnection();
            SqlCommand cmd = new SqlCommand();
            cmd.Connection = con;
            con.Open();
            cmd.CommandText = query;
            cmd.ExecuteNonQuery();
            con.Close();
            MessageBox.Show("Data Processed Successfully.", "Success", MessageBoxButtons.OK, MessageBoxIcon.Information);
        }
    }
}

