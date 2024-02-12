import csv
import matplotlib.pyplot as plt
import tkinter
from tkinter import messagebox

BMI_CATEGORIES = {
    'Underweight': '#F4D9AE',
    'Normal': '#2D8077',
    'Overweight': '#DE9E46',
    'Obesity': '#CD4F41'
}

IMAGE_PATHS = {
    'Obesity': '/Users/antruong/Downloads/warning.png',
    'Overweight': '/Users/antruong/Downloads/warning-2.png',
    'Normal': '/Users/antruong/Downloads/checked.png',
    'Underweight': '/Users/antruong/Downloads/warning-2.png'
}

def bmi_calculation(h,w):
    bmi_value = w / (h * h)
    if bmi_value >= 30:
        return 'Obesity', IMAGE_PATHS['Obesity']
    elif bmi_value > 25:
        return 'Overweight', IMAGE_PATHS['Overweight']
    elif bmi_value > 18.5:
        return 'Normal', IMAGE_PATHS['Normal']
    else:
        return 'Underweight', IMAGE_PATHS['Underweight']
def bmi_calculate():
    a=agebox.get()
    h=float(heighttxt.get())
    w=float(weighttxt.get())
    if heighttxt.get()=='' or weighttxt.get()=='':
        tkinter.messagebox.showwarning(title='Error', message='Height and Weight cannot be blank.')
    else:
        bmi_result, image_path = bmi_calculation(h, w)

        photo = tkinter.PhotoImage(file=image_path)
        result_text.config(text=f'{bmi_result}')
        result_image.config(image=photo)
        result_image.image = photo

        new_entry=[a, h, w, round(w /h ** 2,1), bmi_result]
        load_existing_entries(new_entry)

def load_existing_entries(new_entry):
    try:
        with open('bmi.csv', 'a', newline='') as csvfile:
            csvwrite = csv.writer(csvfile)
            csvwrite.writerow(new_entry)
    except FileNotFoundError:
        # 'a' mode automatically creates the file if it doesn't exist
        with open('bmi.csv', 'a', newline='') as csvfile:
            csvwrite = csv.writer(csvfile)
            csvwrite.writerow(['Age', 'Height', 'Weight', 'BMI Value', 'BMI Result'])
            csvwrite.writerow(new_entry)

def data_visual():
    bmi_result=[]
    with open('bmi.csv', 'r') as csvfile:
        for row in csvfile:
            bmi_result.append(row.split(',')[4].strip())

    colors = [ '#F4D9AE','#2D8077', '#DE9E46', '#CD4F41']
    numbers = [bmi_result.count('Underweight'), bmi_result.count('Normal'),
                bmi_result.count('Overweight'), bmi_result.count('Obesity')]
    total_count = len(bmi_result)

    percentages = [count / total_count * 100 for count in numbers]

    labels = ['Underweight', 'Normal', 'Overweight', 'Obesity']
    fig1, ax1 = plt.subplots()
    ax1.pie(percentages, labels=labels, autopct='%1.1f%%', colors=colors, startangle=90)
    ax1.axis('equal')  # Equal aspect ratio ensures that pie is drawn as a circle.
    plt.title('BMI Demographic')
    plt.show()

if __name__ == '__main__':
    window=tkinter.Tk()
    window.title('BMI Calculator')
    frame=tkinter.Frame(window)
    frame.pack()

    userinfoframe=tkinter.LabelFrame(frame)
    userinfoframe.grid(row=0, column=0, sticky='news')

    agelabel=tkinter.Label(userinfoframe,text='Age: ')
    agelabel.grid(row=0,column=0)

    agebox=tkinter.Spinbox(userinfoframe,from_='1', to='150')
    agebox.grid(row=1,column=0,padx=10)

    heightlabel=tkinter.Label(userinfoframe,text='Height (m): ')
    heightlabel.grid(row=2,column=0)

    heighttxt=tkinter.Entry(userinfoframe)
    heighttxt.grid(row=3,column=0)

    weightlabel=tkinter.Label(userinfoframe,text='Weight (kg): ')
    weightlabel.grid(row=4,column=0,padx=10)

    weighttxt=tkinter.Entry(userinfoframe)
    weighttxt.grid(row=5,column=0)

    cal_button = tkinter.Button(frame, text= 'BMI Calculate', command=bmi_calculate,height='1')
    cal_button.grid(row=6,column=0,padx=10, pady=5)

    demo_button = tkinter.Button(frame, text= 'Show Demographic',command=data_visual, height='1')
    demo_button.grid(row=7,column=0,padx=10, pady=5)

    resultinfoframe=tkinter.LabelFrame(frame)
    resultinfoframe.grid(row=8, column=0, sticky='news')

    result_image= tkinter.Label(resultinfoframe)
    result_image.grid(row=9, column=0)

    result_text= tkinter.Label(resultinfoframe, anchor='center', justify='center')
    result_text.grid(row=9, column=1,sticky='nsew')

    window.mainloop()
