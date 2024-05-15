using System;
using System.Drawing;
using System.Windows.Forms;

namespace MatrixColoring
{
    public partial class Form1 : Form
    {
        private const int MatrixSize = 10;
        private DataGridView dataGridView;

        public Form1()
        {
            InitializeComponent();
            InitializeDataGridView();
            InitializeButtons();
        }

        private void InitializeComponent()
        {
            this.SuspendLayout();
            // Додавання і налаштування компонентів форми
            this.ResumeLayout(false);
        }

        private void InitializeDataGridView()
        {
            dataGridView = new DataGridView
            {
                ColumnCount = MatrixSize,
                RowCount = MatrixSize,
                Dock = DockStyle.Top,
                Height = 250,
                AllowUserToAddRows = false,
                AllowUserToDeleteRows = false,
                RowHeadersVisible = false,
                ColumnHeadersVisible = false
            };

            for (int i = 0; i < MatrixSize; i++)
            {
                dataGridView.ColumnCount = MatrixSize;
                dataGridView.RowCount = MatrixSize;
            }

            this.Controls.Add(dataGridView);
        }

        private void InitializeButtons()
        {
            var buttonPanel = new FlowLayoutPanel
            {
                Dock = DockStyle.Bottom,
                Height = 200
            };

            string[] buttonLabels = {
                "Main Diagonal", "Above Main Diagonal", "Below Main Diagonal",
                "Anti Diagonal", "Above Anti Diagonal", "Below Anti Diagonal",
                "Upper Half", "Lower Half",
                "Left Half", "Right Half"
            };

            foreach (var label in buttonLabels)
            {
                var button = new Button
                {
                    Text = label,
                    AutoSize = true
                };
                button.Click += Button_Click;
                buttonPanel.Controls.Add(button);
            }

            this.Controls.Add(buttonPanel);
        }

        private void Button_Click(object sender, EventArgs e)
        {
            Button button = sender as Button;
            ClearColors();
            switch (button.Text)
            {
                case "Main Diagonal":
                    ColorMainDiagonal();
                    break;
                case "Above Main Diagonal":
                    ColorAboveMainDiagonal();
                    break;
                case "Below Main Diagonal":
                    ColorBelowMainDiagonal();
                    break;
                case "Anti Diagonal":
                    ColorAntiDiagonal();
                    break;
                case "Above Anti Diagonal":
                    ColorAboveAntiDiagonal();
                    break;
                case "Below Anti Diagonal":
                    ColorBelowAntiDiagonal();
                    break;
                case "Upper Half":
                    ColorUpperHalf();
                    break;
                case "Lower Half":
                    ColorLowerHalf();
                    break;
                case "Left Half":
                    ColorLeftHalf();
                    break;
                case "Right Half":
                    ColorRightHalf();
                    break;
            }
        }

        private void ClearColors()
        {
            for (int i = 0; i < MatrixSize; i++)
            {
                for (int j = 0; j < MatrixSize; j++)
                {
                    dataGridView[j, i].Style.BackColor = Color.White;
                }
            }
        }

        private void ColorMainDiagonal()
        {
            for (int i = 0; i < MatrixSize; i++)
            {
                dataGridView[i, i].Style.BackColor = Color.Blue;
            }
        }

        private void ColorAboveMainDiagonal()
        {
            for (int i = 0; i < MatrixSize; i++)
            {
                for (int j = i + 1; j < MatrixSize; j++)
                {
                    dataGridView[j, i].Style.BackColor = Color.Green;
                }
            }
        }

        private void ColorBelowMainDiagonal()
        {
            for (int i = 1; i < MatrixSize; i++)
            {
                for (int j = 0; j < i; j++)
                {
                    dataGridView[j, i].Style.BackColor = Color.Red;
                }
            }
        }

        private void ColorAntiDiagonal()
        {
            for (int i = 0; i < MatrixSize; i++)
            {
                dataGridView[i, MatrixSize - i - 1].Style.BackColor = Color.Purple;
            }
        }

        private void ColorAboveAntiDiagonal()
        {
            for (int i = 0; i < MatrixSize - 1; i++)
            {
                for (int j = 0; j < MatrixSize - i - 1; j++)
                {
                    dataGridView[j, i].Style.BackColor = Color.Orange;
                }
            }
        }

        private void ColorBelowAntiDiagonal()
        {
            for (int i = 1; i < MatrixSize; i++)
            {
                for (int j = MatrixSize - i; j < MatrixSize; j++)
                {
                    dataGridView[j, i].Style.BackColor = Color.Yellow;
                }
            }
        }

        private void ColorUpperHalf()
        {
            for (int i = 0; i < MatrixSize / 2; i++)
            {
                for (int j = 0; j < MatrixSize; j++)
                {
                    dataGridView[j, i].Style.BackColor = Color.Cyan;
                }
            }
        }

        private void ColorLowerHalf()
        {
            for (int i = MatrixSize / 2; i < MatrixSize; i++)
            {
                for (int j = 0; j < MatrixSize; j++)
                {
                    dataGridView[j, i].Style.BackColor = Color.Magenta;
                }
            }
        }

        private void ColorLeftHalf()
        {
            for (int i = 0; i < MatrixSize; i++)
            {
                for (int j = 0; j < MatrixSize / 2; j++)
                {
                    dataGridView[j, i].Style.BackColor = Color.Lime;
                }
            }
        }

        private void ColorRightHalf()
        {
            for (int i = 0; i < MatrixSize; i++)
            {
                for (int j = MatrixSize / 2; j < MatrixSize; j++)
                {
                    dataGridView[j, i].Style.BackColor = Color.Pink;
                }
            }
        }

        [STAThread]
        static void Main()
        {
            Application.EnableVisualStyles();
            Application.SetCompatibleTextRenderingDefault(false);
            Application.Run(new Form1());
        }
    }
}
