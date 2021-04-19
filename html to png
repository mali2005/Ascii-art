using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
using htmltopng.Properties;
using htmltopng;
using System.Threading;
using System.IO;

namespace htmltopng
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        
        static int i = 0;
         
        private void button1_Click(object sender, EventArgs e)
        {
            timer1.Start();   
        }
        
        private void Form1_Load(object sender, EventArgs e)
        {

        }
        Bitmap bitmap;
        private void webBrowser1_DocumentCompleted_1(object sender, WebBrowserDocumentCompletedEventArgs e)
        {
            webBrowser1.Width = webBrowser1.Document.Body.ScrollRectangle.Width;
            webBrowser1.Height = webBrowser1.Document.Body.ScrollRectangle.Height;

            bitmap = new Bitmap(webBrowser1.Width, webBrowser1.Height);
            webBrowser1.DrawToBitmap(bitmap, new Rectangle(0, 0, webBrowser1.Width, webBrowser1.Height));
            bitmap.Save(string.Format("out\\ck{0}.png",i));
        }
        
        private void timer1_Tick(object sender, EventArgs e)
        {
            StreamReader reader = new StreamReader(string.Format("render\\is{0}.html",i));
            webBrowser1.DocumentText = reader.ReadToEnd();
            i++;
        }
    }
}
