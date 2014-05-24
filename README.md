ResimUpload
===========

//Asp.Net FileUpload ve Resim boyutlandırma

        protected void btnfotoekle_Click(object sender, EventArgs e)
        {
            Random rastgele=new Random();
            int sayi=rastgele.Next(100,10000);
            string resimadi = "";
            string uzanti = "";
            string resimdizin1 = "../Resimler/Boyut/";
            string resimdizin2 = "../Resimler/Orjinal/";
            if (FUResim.HasFile)
            {
                uzanti = Path.GetExtension(FUResim.PostedFile.FileName);
                resimadi = "AOguzhan_" + "Foto_" + sayi;
                FUResim.SaveAs(Server.MapPath("../Resimler/Orjinal/" + resimadi + uzanti));
                Bitmap bmp = new Bitmap(Server.MapPath("../Resimler/Orjinal/" + resimadi + uzanti));
                using (Bitmap OrjinalResim = bmp)
                {
                    double ResYukseklik = 360;
                    double ResGenislik = 900;
                    Size yenidegerler = new Size(Convert.ToInt32(ResGenislik), Convert.ToInt32(ResYukseklik));
                    Bitmap yeniresim = new Bitmap(OrjinalResim, yenidegerler);
                    yeniresim.Save(Server.MapPath("../Resimler/Boyut/" + resimadi + uzanti));
                    yeniresim.Dispose();
                    OrjinalResim.Dispose();
                    bmp.Dispose();
                }
            }
        }
