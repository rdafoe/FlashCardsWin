using System;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;
using System.Resources;
using System.Reflection;
using System.IO;

namespace MedTermsFlashCardApplication
{
    public partial class Form1 : Form
    {
        bool initialLoad = true;
        int termIndex = 0;
        bool alphabetical = true;
        string[] showTermArray;
        string importFilePath;
        DirectoryInfo myfolder;
        

        public Form1()
        {
            InitializeComponent();
            load();
        }

        private void load()
        {
            toolStripComboBox1.Items.Clear();
            toolStripComboBox1.Text = null;
            toolStripComboBox2.Items.Clear();
            toolStripComboBox2.Text = null;

            this.myfolder = new DirectoryInfo(Directory.GetCurrentDirectory());

            //get all file in folder with .txt extension
            FileInfo[] strFiles = this.myfolder.GetFiles("*.txt");

            //for each file add to combobox
            foreach (FileInfo myItem in strFiles)
            {
                toolStripComboBox1.Items.Add(myItem);
                toolStripComboBox2.Items.Add(myItem);
            }
            toolStripComboBox1.SelectedIndex = 0;
            toolStripComboBox2.SelectedIndex = 0;

            this.buttonShowAnswer.Focus();
            initialLoad = false;
        }

        private void Display()
        {
            this.labelCount.Text = FileHandling.Count().ToString();
            showTermArray = FileHandling.ShowTerm(out termIndex, termIndex);
            labelTerm.Text = showTermArray[0].ToString();

            if (showTermArray[0].ToString() == "Congratulations!")
            {
                labelAnswer.Text = showTermArray[1].ToString();
                //labelAnswer.Visible = true;
                // Set the alignment of the text that follows.
                labelAnswer.SelectionAlignment = HorizontalAlignment.Center;

            }
        }

        private void buttonShowAnswer_Click(object sender, EventArgs eArg)
        {
            Display();
            try
            {
                labelAnswer.Text = showTermArray[1].ToString();
                //labelAnswer.Visible = true;
                labelAnswer.SelectionAlignment = HorizontalAlignment.Center;
            }
            catch (Exception e)
            {
                MessageBox.Show("Oooppps, Sorry. I've ran into a problem" + "\n" + e.Message, "Read Data Error");
            }
        }

        private void buttonNext_Click(object sender, EventArgs e)
        {
            labelAnswer.Clear();
            ++termIndex;
            Display();
            this.buttonShowAnswer.Focus();
        }

        private void buttonPrevious_Click(object sender, EventArgs e)
        {
            labelAnswer.Clear();
            --termIndex;
            Display();
            this.buttonShowAnswer.Focus();
        }

        private void Form1_KeyPress(object sender, KeyPressEventArgs e)
        {
            if (e.KeyChar == 13 && showTermArray.Length > 0)
            {
                buttonShowAnswer_Click(this, null);
            }
        }

        private void AlphabeticalToolStripMenuItem2_Click(object sender, EventArgs e)
        {
            if (!(alphabetical))
            {
                FileHandling.AlphabeticalList();
                alphabetical = true;
                Display();
                this.alphabeticalStatusLabel.Image = new Bitmap(MedTermsFlashCardApplication.Properties.Resources.alphabetical);

            }
        }

        private void jumbledToolStripMenuItem_Click(object sender, EventArgs e)
        {
            if (alphabetical)
            {
                FileHandling.ShuffleGenericList<String>();
                alphabetical = false;
                this.alphabeticalStatusLabel.Image = new Bitmap(MedTermsFlashCardApplication.Properties.Resources.jumbled);
            }
        }


        private void buttonGotIt_Click(object sender, EventArgs e)
        {
            FileHandling.RemoveWordFromList(termIndex);
            labelAnswer.Clear();
            Display();
        }

        /// <summary>
        /// Choose file to load
        /// </summary>
        /// <param name="sender"></param>
        /// <param name="e"></param>
        private void toolStripComboBox1_SelectedIndexChanged(object sender, EventArgs e)
        {
            string file = toolStripComboBox1.SelectedItem.ToString();
            labelAnswer.Clear();
            FileHandling.LoadFile(file);
            Display();
            this.toolStripStatusLabel4.Text = "Word Units from: " + (toolStripComboBox1.SelectedItem.ToString());
        }

        /// <summary>
        /// Choose file to edite
        /// </summary>
        /// <param name="sender"></param>
        /// <param name="e"></param>
        private void toolStripComboBox2_SelectedIndexChanged(object sender, EventArgs e)
        {
            if (!(initialLoad))
            {
                ToolStripComboBox editFile = (ToolStripComboBox)sender;
                FileHandling.EditFile(editFile.SelectedItem.ToString());
            }

        }

        private void toolStripMenuItem4_Click(object sender, EventArgs e)
        {
            openFileDialog1.Filter = "txt files (*.txt)|*.txt";

            if (this.openFileDialog1.ShowDialog() == DialogResult.OK)
            {
                this.importFilePath = this.openFileDialog1.FileName;
                string file = this.importFilePath.Substring(this.importFilePath.LastIndexOf('\\') + 1);//, this.importFilePath.LastIndexOf('.'));
                File.Copy(this.importFilePath, myfolder + "\\" + file, true);
                toolStripComboBox1.Items.Add(file);
                this.load();
            }
        }
        
        private void aboutToolStripMenuItem_Click(object sender, EventArgs e)
        {
            PictureBox splashImage = new PictureBox();
            Form aboutFrm = new Form();
            aboutFrm.ClientSize = new System.Drawing.Size(600, 400);
            aboutFrm.Controls.Add(splashImage);

            splashImage.ClientSize = new System.Drawing.Size(600, 400);
            splashImage.BringToFront();
            splashImage.BackgroundImage = new Bitmap(MedTermsFlashCardApplication.Properties.Resources.Splash);
            splashImage.Show();
            aboutFrm.ShowDialog();
        }
    }
}
