# -*- coding: utf-8 -*-
"""
Created on Thu Mar  6 19:30:24 2025

@author: Shree
"""

import pickle
import streamlit as st

st.title("Survival prediction")

load = open('LRmodel.pkl','rb')
model = pickle.load(load)

# Define predict function 
def predict(Pclass, Age, SibSp, Parch, Fare, Sex_male, Embarked_Q, Embarked_S):
    prediction = model.predict([[Pclass, Age, SibSp, Parch, Fare, Sex_male, Embarked_Q, Embarked_S]]) 
    # pass arguments in 2 dimensions using 2 square brackets
    return prediction

def main():
    st.title('Titanic passanger survival prediction')
    # Accept input values from user through browser
    Pclass = st.number_input('Pclass: ')
    Age = st.number_input('Age: ')    
    SibSp = st.number_input('SibSp: ')
    Parch = st.number_input('Parch:')
    Fare = st.number_input('Fare: ')
    Sex_male = st.number_input('Sex_male: ')
    Embarked_Q = st.number_input('Embarked_Q: ')
    Embarked_S = st.number_input('Embarked_S ')
    
    if st.button('Predict'): # if predict button is clicked then execute below code
         result = predict(Pclass, Age, SibSp, Parch, Fare, Sex_male, Embarked_Q, Embarked_S)
         if result==0:
             st.success("Survived")
         else:
             st.success("Not Survived")
             
if __name__ == '__main__':
    main()
