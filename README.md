# Rectangle_
-Lib

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    namespace RectangleAreaLibrary
    {
        public class GeometryRectangle
        {
            /// <summary>
            /// Вычисление площади прямоугольника по двум сторонам
            /// </summary>
            /// <param name="width"></param>
            /// Ширина прямоугольника 
            /// <param name="height"></param>
            /// <returns>
            /// Площадь прямоугольника
            /// </returns>
            public double RectangleArea(string width, string height)
            {
                double numbers;
                width = width.Replace('.', ',');
                height = height.Replace(".", ",");
                bool result = double.TryParse(width, out numbers);
                bool res = double.TryParse(height, out numbers);
                if (!result || !res)
                {
                    throw new Exception("Введите недопустимые символы");
                }
                if (width == string.Empty || height == string.Empty)
                {
                    throw new Exception("Не введена сторона прямоугольника");
                }
                if (Convert.ToDouble(width) <= 0 || Convert.ToDouble(height) <= 0)
                {
                    throw new Exception("Длины сторон должны иметь положительные значения");
                }
                return Convert.ToDouble(width) * Convert.ToDouble(height); 
            }
        }
    }
-test

    using Microsoft.VisualStudio.TestTools.UnitTesting;
    using System;
    using RectangleAreaLibrary;
    
    namespace RectangleAreaLibraryTests
    {
        [TestClass]
        public class GeometryRectangleTests
        {/// <summary>
        /// Первая сторона - положительное целое число,
        /// вторая сторона - положительное целое число
        /// </summary>
            [TestMethod]
            public void RectangleArea_3and5_15returned()
            {
                //Arrange
                string width = "3";
                string height = "5";
                double expected = 15;
                //Act
                GeometryRectangle obj = new GeometryRectangle();
                double actual = obj.RectangleArea(width, height);
                //Assert
                Assert.AreEqual(expected, actual);
            }
            [TestMethod]
            public void RectangleArea_05and05_025returned()
            {
                //Arrange
                string width = "0,5";
                string height = "0.5";
                double expected = 0.25;
                //Act
                GeometryRectangle obj = new GeometryRectangle();
                double actual = obj.RectangleArea(width, height);
                //Assert
                Assert.AreEqual(expected, actual);
            }
            [TestMethod]
            public void RectangleArea_05and1_05returned()
            {
                //Arrange
                string width = "0,5";
                string height = "1";
                double expected = 0.5;
                //Act
                GeometryRectangle obj = new GeometryRectangle();
                double actual = obj.RectangleArea(width, height);
                //Assert
                Assert.AreEqual(expected, actual);
            }
            [TestMethod]
            public void RectangleArea_01and05_05returned()
            {
                //Arrange
                string width = "1";
                string height = "0.5";
                double expected = 0.5;
                //Act
                GeometryRectangle obj = new GeometryRectangle();
                double actual = obj.RectangleArea(width, height);
                //Assert
                Assert.AreEqual(expected, actual);
            }
            [TestMethod]
            public void RectangleArea_2000and1_05returned()
            {
                //Arrange
                string width = "2,12345678912345678912";
                string height = "5";
                double expected = 10.6172839456;
                //Act
                GeometryRectangle obj = new GeometryRectangle();
                double actual = obj.RectangleArea(width, height);
                //Assert
                Assert.AreEqual(expected, actual);
            }
                /// <summary>
                /// Сторона прямоугольника задана отрицательным числом
                /// </summary>
                [TestMethod]
            public void RectangleArea_NegativeData_ThrowReturned()
            {
                //Arrange
                string width = "-3";
                string height = "5";
                //Act
                GeometryRectangle obj = new GeometryRectangle();
                //Assert
                Assert.ThrowsException<Exception>(()=>obj.RectangleArea(width, height));
            }
            [TestMethod]
            public void RectangleArea_NullOrEmpty()
            {
                //Arrange
                string width = "0";
                string height = "0";
                GeometryRectangle obj = new GeometryRectangle();
                Assert.ThrowsException<Exception>(() => obj.RectangleArea(width, height));
            }
            [TestMethod]
            public void RectangleArea_WrongValue()
            {
                string width = " ";
                string height = "4";
                GeometryRectangle obj = new GeometryRectangle();
                Assert.ThrowsException<Exception>(() => obj.RectangleArea(width, height));
            }
            [TestMethod]
            public void RectangleArea_WrongValue1()
            {
                string width = "4";
                string height = " ";
                GeometryRectangle obj = new GeometryRectangle();
                Assert.ThrowsException<Exception>(() => obj.RectangleArea(width, height));
            }
            [TestMethod]
            public void RectangleArea_WrongValue2()
            {
                string width = "-1";
                string height = "5,5";
                GeometryRectangle obj = new GeometryRectangle();
                Assert.ThrowsException<Exception>(() => obj.RectangleArea(width, height));
            }
            [TestMethod]
            public void RectangleArea_WrongValue3()
            {
                string width = "-1,5";
                string height = "-5.5";
                GeometryRectangle obj = new GeometryRectangle();
                Assert.ThrowsException<Exception>(() => obj.RectangleArea(width, height));
            }
            [TestMethod]
            public void RectangleArea_WrongValue4()
            {
                string width = "3п";
                string height = "5";
                GeometryRectangle obj = new GeometryRectangle();
                Assert.ThrowsException<Exception>(() => obj.RectangleArea(width, height));
            }
        }
    }
