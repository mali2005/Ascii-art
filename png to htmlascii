using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
using System.IO;
using MediaToolkit;
using MediaToolkit.Model;
using MediaToolkit.Options;

namespace ascii
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }
        private string[] _AsciiChars = { "#", "#", "@", "%", "=", "+", "*", ":", "-", ".", "&nbsp;" };

        private Bitmap GetReSizedImage(Bitmap inputBitmap, int asciiWidth)

        {

            int asciiHeight = 0;



            asciiHeight = (int)Math.Ceiling((double)inputBitmap.Height * asciiWidth / inputBitmap.Width);





            Bitmap result = new Bitmap(asciiWidth, asciiHeight);

            Graphics g = Graphics.FromImage((Image)result);



            g.InterpolationMode = System.Drawing.Drawing2D.InterpolationMode.HighQualityBicubic;

            g.DrawImage(inputBitmap, 0, 0, asciiWidth, asciiHeight);

            g.Dispose();

            return result;

        }
        private string ConvertToAscii(Bitmap image)

        {

            Boolean toggle = false;

            StringBuilder sb = new StringBuilder();



            for (int h = 0; h < image.Height; h++)

            {

                for (int w = 0; w < image.Width; w++)

                {

                    Color pixelColor = image.GetPixel(w, h);



                    int red = (pixelColor.R + pixelColor.G + pixelColor.B) / 3;

                    int green = (pixelColor.R + pixelColor.G + pixelColor.B) / 3;

                    int blue = (pixelColor.R + pixelColor.G + pixelColor.B) / 3;

                    Color grayColor = Color.FromArgb(red, green, blue);





                    if (!toggle)

                    {

                        int index = (grayColor.R * 10) / 255;

                        sb.Append(_AsciiChars[index]);

                    }

                }

                if (!toggle)

                {

                    sb.Append("<BR>");

                    toggle = true;

                }

                else

                {

                    toggle = false;

                }

            }

            return sb.ToString();

        }
        string _Content;
        private void button1_Click(object sender, EventArgs e)
        {
            Bitmap bitmap;
            Bitmap image;
            button1.Enabled = false;
            OpenFileDialog file = new OpenFileDialog();
            file.Filter = "Resim |*.png| Resim|*.jpg";
            file.FilterIndex = 2;
            file.RestoreDirectory = true;
            file.CheckFileExists = false;
            file.Multiselect = true;
            file.Title = "Resimleri Seçiniz";
            int i = 0;
            if (file.ShowDialog() == DialogResult.OK)
            {
                foreach (String fle in file.FileNames)
                {
                    image = new Bitmap(fle, true);
                    image = GetReSizedImage(image, this.trackBar1.Value);
                    _Content = ConvertToAscii(image);                    
                    StreamWriter writer = File.AppendText(string.Format("render\\is{0}.html", i));
                    writer.Write("<pre>" + _Content + "</pre>");
                    writer.Close();
                    writer.Dispose();
                    i++;
                }
            }
            button1.Enabled = true;



        }

        private void Form1_Resize(object sender, EventArgs e)
        {
            webBrowser1.Width = this.Width - 121;
            webBrowser1.Height = this.Height - 115;
            trackBar1.Location = new Point(12, this.Height - 96);
        }



        private void Form1_Load(object sender, EventArgs e)
        {
            Control.CheckForIllegalCrossThreadCalls = false;
        }

        private void button3_Click(object sender, EventArgs e)
        {
            FolderBrowserDialog folderDlg = new FolderBrowserDialog();
            folderDlg.ShowNewFolderButton = true;
            // Show the FolderBrowserDialog.  
            DialogResult result = folderDlg.ShowDialog();
            if (result == DialogResult.OK)
            {
                Environment.SpecialFolder root = folderDlg.RootFolder;
                webBrowser1.Width = webBrowser1.Document.Body.ScrollRectangle.Width;
                webBrowser1.Height = webBrowser1.Document.Body.ScrollRectangle.Height;

                Bitmap bitmap = new Bitmap(webBrowser1.Width, webBrowser1.Height);
                webBrowser1.DrawToBitmap(bitmap, new Rectangle(0, 0, webBrowser1.Width, webBrowser1.Height));
                bitmap.Save(folderDlg.SelectedPath + "//çıktı.png");
            }

        }

        
    }
}
