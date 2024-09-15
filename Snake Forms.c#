using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;


namespace Snake_v2
{
    public partial class Snake : Form
    {
        List<PictureBox> List = new List<PictureBox>();
        int move = 55;    
        PictureBox food = new PictureBox();
        String Direction = "right";
        int score = 0;
        int finalscore = 0;
        bool timerjede = false;
        bool znova = false;
        int mode=1;
        int realmode = 1;
        
        public Snake()
        
        {
            
            InitializeComponent();
            
            GameStart();
        }

        public void GameStart()
        {
            if (timerjede == true)
            {
                mode = realmode;
            }
           
            
            if (mode == 1)
            {
                MODEINFO.Text = "GAME MODE: SPEED";
            }
            if (mode == 2)
            {
                MODEINFO.Text = "GAME MODE: COLLECTOR";
            }

            MODEINFO.Left -= 50;   
            
            if (timerjede == false)
            {
                timer1.Enabled = false;
            }
            else
            {
                timer1.Enabled = true;
            }
            if (timer1.Enabled == false)
            {
                pbstart.Visible = true;
                lblstart.Visible = true;
            }

           
            score = 0;
            
            Direction = "right";
            timer1.Interval = 200;
            lblScore.Text = "0";
            List = new List<PictureBox>();
            for (int i = 1; 0 <= i; i--)
            {
                CreateSnake(List, this, (i * move) + 70, 80);
            }
            FoodGenerator();
        }

        public void CreateSnake(List<PictureBox> ListParticles, Form formular, int positionx, int positiony)
        {
            PictureBox pb = new PictureBox();
            pb.Location = new Point(positionx, positiony);
            pb.Image = Image.FromFile(@"C:\Users\malus\source\repos\Snake v2\Snake v2\Resources\particle.png");
            pb.BackColor = Color.Transparent;
            pb.Width = move;
            pb.Height = move;
            pb.SizeMode = PictureBoxSizeMode.AutoSize;
            ListParticles.Add(pb);
            formular.Controls.Add(pb);
        }

        private void FoodGenerator()
        {
            Random rnd = new Random();
            int value = rnd.Next(1, 14);
            int foodx = 55*value+14;
            value = rnd.Next(1, 14);
            int foody = 55 * value + 24;
            PictureBox pb = new PictureBox();
            pb.Location = new Point(foodx, foody);
            pb.Image = Image.FromFile(@"C:\Users\malus\source\repos\Snake v2\Snake v2\Resources\cherry.png");
            pb.BackColor = Color.Transparent;
            pb.SizeMode = PictureBoxSizeMode.AutoSize;
            food = pb;
            this.Controls.Add(pb);
            score += 100;
            if (score > finalscore) { finalscore = score; }
            lblScore.Text = "Score: " + finalscore.ToString();

        }

       
        private void Movement(object sender, KeyEventArgs e)
        { 
                Direction = ((e.KeyCode & Keys.Up) == Keys.Up) ? "up" : Direction;
                Direction = ((e.KeyCode & Keys.Down) == Keys.Down) ? "down" : Direction;
                Direction = ((e.KeyCode & Keys.Left) == Keys.Left) ? "left" : Direction;
                Direction = ((e.KeyCode & Keys.Right) == Keys.Right) ? "right" : Direction;
            

            if (e.KeyCode == Keys.Enter) { timer1.Enabled = true; timerjede = true; }
            if (timer1.Enabled == true)
            {
                TEXTMODE1.Visible = false;
                TEXTMODE2.Visible = false;
                pbstart.Visible = false;
                lblstart.Visible = false;
            }
            if (e.KeyCode == Keys.T)
            {
                znova = true;
            }

            if (e.KeyCode == Keys.S)
            {
                realmode = 1;           
            }
            if (e.KeyCode == Keys.C)
            {
                realmode = 2;
            }
            
        }

        private void timer1_Tick(object sender, EventArgs e)
        {
            
            int interval = timer1.Interval;
            if (mode == 1)
            {
                if (List.Count < 10)
                {
                    timer1.Interval = 250 - 10 * List.Count;
                }
                else
                {
                    timer1.Interval = 150 - 7 * (List.Count - 10);
                }
            }
            if (mode == 2)
            {
                timer1.Interval = 230;
            }
           
            
            int nx = List[0].Location.X;
            int ny = List[0].Location.Y;
            List[0].Image = Image.FromFile(@"C:\Users\malus\source\repos\Snake v2\Snake v2\Resources\head" + Direction + ".png");

            for (int i = List.Count - 1; i >= 0; i--)
            {
                if (i == 0)
                {
                    if (Direction == "right") nx = nx + move;
                    else if (Direction == "left") nx = nx - move;
                    else if (Direction == "down") ny = ny + move;
                    else if (Direction == "up") ny = ny - move;
                    List[0].Image = Image.FromFile(@"C:\Users\malus\source\repos\Snake v2\Snake v2\Resources\head" + Direction + ".png");
                    List[0].Location = new Point(nx, ny);
                }
                else
                {
                    List[i].Location = new Point((List[i - 1].Location.X), (List[i].Location.Y));
                    List[i].Location = new Point((List[i].Location.X), (List[i - 1].Location.Y));
                }
            }
            
            if (List[0].Bounds.IntersectsWith(food.Bounds))
            {
                this.Controls.Remove(food);
                
                
                FoodGenerator();
                CreateSnake(List, this, List[List.Count - 1].Location.X * move, 0);
            }
            
            if (List[0].Top < 10 || List[0].Top > 900||List[0].Left<10||List[0].Left>900)
            {
                Reset();
            }
            for (int particlecounter = 1; particlecounter < List.Count; particlecounter++)
            {
                if (List[0].Bounds.IntersectsWith(List[particlecounter].Bounds))
                {
                    Reset();
                }

            }

        }

        public void Reset()
        {
            if (mode == 1)
            {
                MODEINFO.Text = "GAME MODE: SPEED";
            }
            if (mode == 2)
            {
                MODEINFO.Text = "GAME MODE: COLLECTOR";
            }
            TEXTMODE1.Visible = true;
            TEXTMODE2.Visible = true;
            gotext.Visible = true;
            lblT.Visible = true;
            gotext.BackColor = Color.Transparent;
            gopb.Visible = true;
            
            lblScore.Top = 404;
            lblScore.Left=412;
            foreach (PictureBox Snake in List) { this.Controls.Remove(Snake); }
            this.Controls.Remove(food);
            if (znova == true)
            {
                TEXTMODE1.Visible = false;
                TEXTMODE2.Visible = false;
                gotext.Visible = false;
                lblT.Visible = false;
                gopb.Visible = false;
                znova = false;
                score = 0;
                finalscore = 0;
                lblScore.Top = 7;
                lblScore.Left = 42;
                GameStart();
            }

        }
    }
    

}

