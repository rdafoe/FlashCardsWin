using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
using System.Windows.Forms;

namespace MedTermsFlashCardApplication
{
    class FileHandling
    {
        public static List<string> terms = new List<string>();

        public static List<string> LoadFile(string fileName)
        {
            terms.Clear();

            try
            {
                using (StreamReader s = new StreamReader(fileName))
                {
                    string t;
                    while ((t = s.ReadLine()) != null)
                    {
                        terms.Add(t);
                    }
                }
            }
            catch (Exception e)
            {
                MessageBox.Show(e.Message);
            }

            return terms;
        }

        public static void EditFile(string fileName)
        {
            try
            {
                System.Diagnostics.Process.Start(fileName);
            }
            catch (Exception ex)
            {
                MessageBox.Show(ex.Message, "Error opening File");
            }
        }

        public static string[] ShowTerm(out int termIndex, int val)
        {  
            termIndex = val;

            string[] temp = null;

            try
            {
                if (terms.Count > termIndex && termIndex > 0)//there are terms and greater than 0
                {
                    temp = terms[termIndex].Split(',');
                }
                else if (terms.Count < termIndex || termIndex < 0)//wrap to end of list
                {
                    termIndex = terms.Count - 1;
                    temp = terms[termIndex].Split(',');
                }
                else if (terms.Count == 0 || terms.Count < 0)
                {
                    temp = new string[] { "Congratulations!", "List Mastered!" };
                }
                else//start from beginning of list
                {
                    termIndex = 0;
                    temp = terms[termIndex].Split(',');
                }
            }
            catch (Exception ex)
            {
                MessageBox.Show(ex.Message, "Error!");
            }

            return temp;
        }

        public static void AlphabeticalList()
        {
            terms.Sort();
        }

        /// <summary>
        /// method for shuffling the term list
        /// </summary>
        public static void ShuffleGenericList<String>()
        {
            //generate a Random instance
            Random rnd = new Random();
            //get the count of items in the list
            int i = terms.Count();
            //do we have a reference type or a value type
            string val = default(string);

            //we will loop through the list backwards
            while (i >= 1)
            {
                //decrement our counter
                i--;
                //grab the next random item from the list
                var nextIndex = rnd.Next(i, terms.Count());
                val = terms[nextIndex];
                //start swapping values
                terms[nextIndex] = terms[i];
                terms[i] = val;
            }
        }

        public static int RemoveWordFromList(int index)
        {
            try
            {
                terms.Remove(terms[index]);
            }
            catch(Exception ex)
            {
                MessageBox.Show(ex.Message, "Error removing item from study list");
            }
            
            return terms.Count;
        }

        public static int Count()
        {
            return terms.Count;
        }
    }
}
