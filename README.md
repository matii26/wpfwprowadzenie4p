# wpfwprowadzenie4p

<Window x:Class="wprowadzenie.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:wprowadzenie"
        mc:Ignorable="d"
        Title="MainWindow PESEL:XXXXXXXXXXX" Height="450" Width="800">
    <Grid>
        <Grid.ColumnDefinitions>
            <ColumnDefinition Width="*"></ColumnDefinition>
            <ColumnDefinition Width="*"></ColumnDefinition>
        </Grid.ColumnDefinitions>
        <Grid.RowDefinitions>
            <RowDefinition Height="*"></RowDefinition>
            <RowDefinition Height="auto"></RowDefinition>
        </Grid.RowDefinitions>
        <StackPanel>
            <GroupBox Header="Rodzaj przesyłki" Margin="10">
                <StackPanel Margin="10">
                    <RadioButton GroupName="rodzaj" x:Name="pocztowka_radio" IsChecked="True" >
                        Pocztówka
                    </RadioButton>
                    <RadioButton GroupName="rodzaj" x:Name="list_radio" >
                        List
                    </RadioButton>
                    <RadioButton GroupName="rodzaj" x:Name="paczka_radio">
                        Paczka
                    </RadioButton>
                </StackPanel>
            </GroupBox>
            <Button Margin="10" Click="Button_Click">Sprawdź cenę</Button>
            <StackPanel Orientation="Horizontal">
                <Image x:Name="obraz" Source="pocztowka.png" Margin="10"></Image>
                <TextBlock Margin="10" x:Name="cena_txt">Cena</TextBlock>
            </StackPanel>
        </StackPanel>
        <GroupBox Header="Dane adresowe" Grid.Column="1">
            <StackPanel>
                <TextBlock>Ulica z numerem</TextBlock>
                <TextBox></TextBox>
                <TextBlock>Kod pocztowy</TextBlock>
                <TextBox x:Name="kod_txt"></TextBox>
                <TextBlock>Miasto</TextBlock>
                <TextBox></TextBox>
            </StackPanel>
        </GroupBox>
        <Button Grid.Row="1" Grid.ColumnSpan="2" Margin="10" Click="Button_Click_1">Zatwierdź</Button>
    </Grid>
</Window>





using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Data;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Imaging;
using System.Windows.Navigation;
using System.Windows.Shapes;

namespace wprowadzenie
{
    /// <summary>
    /// Interaction logic for MainWindow.xaml
    /// </summary>
    public partial class MainWindow : Window
    {
        public MainWindow()
        {
            InitializeComponent();
        }

        private void Button_Click(object sender, RoutedEventArgs e)
        {
            if(list_radio.IsChecked == true)
            {
                obraz.Source = new BitmapImage(new Uri("list.png",UriKind.Relative));
                cena_txt.Text = "Cena: 1.5zł";
            }
            if (pocztowka_radio.IsChecked == true)
            {
                obraz.Source = new BitmapImage(new Uri("pocztowka.png", UriKind.Relative));
                cena_txt.Text = "Cena: 1zł";
            }
            if (paczka_radio.IsChecked == true)
            {
                obraz.Source = new BitmapImage(new Uri("paczka.png", UriKind.Relative));
                cena_txt.Text = "Cena: 10zł";
            }
        }

        private void Button_Click_1(object sender, RoutedEventArgs e)
        {
            string kodPocztowy = kod_txt.Text;
            if (kodPocztowy.Length != 5)
            {
                MessageBox.Show("NIeprawidłowa liczba znaków");
            }
            else if (czySameCyfry(kodPocztowy) == false)
            {
                MessageBox.Show("Kod pocztowy powinien składać się z samych cyfr");
            }
            else
            {
                MessageBox.Show("Dane przesyłki zostały wprowadzone");
            }
        }
        private bool czySameCyfry(string tekst)
        {
            for(int i = 0; i < tekst.Length; i++)
            {
                if("0123456789".Contains(tekst[i])==false)
                {
                    return false;
                }
            }




            return true;
        }
    }
}

