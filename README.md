import PySimpleGUI as sg
import pandas as pd

sg.theme("Dark")

EXCEL_FILE = "Pendaftaran.xlsx"

df = pd.read_excel(EXCEL_FILE)

layout={
{sg.Text('Masukan Data Kamu: ')},
{sg.Text('Nama',size=(15,1)), sg.inputText(key='Nama')},
{sg.Text('No Telp',size=(15,1)), sg.inputText(key='Tlp')},
{sg.Text('Alamat',size=(15,1)), sg.Multiline(key='Alamat')},
{sg.Text('Tgl Lahir',size=(15,1)), sg.inputText(key='Tgl Lahir'),
                            sg.CalenderButton('Kalender', target='Tgl Lahir', format=('%d-%M-%Y'))},
{sg.Text('Jenis kelamin',size=(15,1)), sg.Combo({'pria','wanita'},key='jekel')},
{sg.Text('Hobi',size=(15,1)), sg.Checkbox('belajar',key='belajar'),
                                sg.Checkbox('Menonton',key='Menonton'),
                                sg.Checkbox('musik',key='musik')},
{sg.submit(), sg.Button('clear'), sg.Exit()}

}

window=sg.window('Form pendaftaran',layout)

def clear_input():
    for key in values:
        window[key]('')
        return None

while True :
    event, values = window.read()
    if event == sg.WIN_CLOSED or event == "EXIT":
        break
    if event == "clear":
        clear_input()
    if event == "submit":
        df =df.append(values, ignore_index=true)
        df.to_excel(EXCEL_FILE, index=false)
        sg.popup('Data Berhasil Di Simpan')
        clear_input()
    window.close()
