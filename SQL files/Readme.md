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

Function c# file for SQL functions:-

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

