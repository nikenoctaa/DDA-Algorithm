# DDA-Algorithm
//Make line using DDA Algorithm
// ddaAlgorithm.cpp : Defines the entry point for the console application.
//

#include "stdafx.h"
// Algoritma DDA

#include <GL\freeglut.h>
#include <GL\glut.h>
#include <iostream>

using namespace std;

//identifier fungsi
void init();
void display(void);
void dda(int x1, int x2, int y1, int y2);

//  posisi window di layar
int window_x;
int window_y;

//  ukuran window
int window_width = 480;
int window_height = 480;

//  judul window
char *judul_window = "Algoritma DDA";

void main(int argc, char **argv)
{
	//  inisialisasi GLUT (OpenGL Utility Toolkit)
	glutInit(&argc, argv);
	// set posisi window supaya berada di tengah 
	window_x = (glutGet(GLUT_SCREEN_WIDTH) - window_width) / 2;
	window_y = (glutGet(GLUT_SCREEN_HEIGHT) - window_height) / 2;
	glutInitWindowSize(window_width, window_height); //set ukuran window 
	glutInitWindowPosition(window_x, window_y); //set posisi window

	glutInitDisplayMode(GLUT_RGBA | GLUT_DOUBLE); // set display RGB dan double buffer
	glutCreateWindow(judul_window);


	init();

	glutDisplayFunc(display); // fungsi display
	glutMainLoop(); // loop pemrosesan GLUT
}

void init()
{
	glClearColor(0.0, 0.0, 0.0, 0.0); //set warna background 
	glColor3f(0.0, 1.0, 0.0); //set warna titik
	glPointSize(5.0); //set ukuran titik
	glMatrixMode(GL_PROJECTION); //set mode matriks yang digunakan 
	glLoadIdentity(); // load matriks identitas
	gluOrtho2D(0.0, 600.0, 0.0, 600.0); // set ukuran viewing window
}
void display(void)
{
	int x1, y1, x2, y2;
	cout << "Masukkan Titik Awal: ";
	cin >> x1 >> y1;

	cout << "Masukkan Titik Akhir: ";
	cin >> x2 >> y2;

	glClear(GL_COLOR_BUFFER_BIT); //clear color
	dda(x1,y1,x2,y2); //panggil fungsi dda 
	glutSwapBuffers(); //swap buffer
	glClear(GL_COLOR_BUFFER_BIT); //clear color

}

void dda(int x1, int y1, int x2, int y2) {
	//int x1, y1, x2, y2;
	float x, y, dx, dy, xend, yend, steps, x_inc, y_inc;
	//tentukan titik awal dan akhir
	//x1 = 100;
	//x2 = 100;
	//y1 = 800;
	//y2 = 100;

	//hitung dx dan dy
	if (x1 > x2) {
		x = x2;
		y = y2;
		xend = x1;
		dx = x1 - x2;
		dy = y1 - y2;
	}
	else if ((x1 == x2) && (y1 < y2)) {
		x = x1;
		y = y1;
		yend = y2;
		dx = x2 - x1;
		dy = y2 - y1;
	}
	else if ((x1 == x2) && (y1 > y2)) {
		x = x2;
		y = y2;
		yend = y1;
		dx = x1 - x2;
		dy = y1 - y2;
	}
	else if ((y1 == y2) && (x1 < x2)) {
		x = x1;
		y = y1;
		xend = x2;
		dx = x2 - x1;
		dy = y2 - y1;
	}
	else if ((y1 == y2) && (x1 > x2)) {
		x = x2;
		y = y2;
		xend = x1;
		dx = x1 - x2;
		dy = y1 - y2;
	}
	else
	{
		x = x1;
		y = y1;
		xend = x2;
		dx = x2 - x1;
		dy = y2 - y1;
	}

	//hitung steps
		if (dx > dy) {
			steps = dx;
		}
		else steps = dy;


	//hitung perubahan nilai x (x_inc) dan y (y_inc)
	x_inc = dx / steps;
	y_inc = dy / steps;

	//gambar titik awal
	glBegin(GL_POINTS);
	glVertex2i(x, y); // gambar titik awal

					  //perulangan untuk menggambar titik-titik 
	if ((dy == 0) && (x1<x2)) {
		do {
			x += x_inc; // x = x + x_inc
			y += y_inc; // y = y + y_inc
			glVertex2i(round(x), round(y)); //gambar titik
		} while (x < xend);
	}
	else if ((dx == 0) && (y1<y2)) {
		do {
			x += x_inc; // x = x + x_inc
			y += y_inc; // y = y + y_inc
			glVertex2i(round(x), round(y)); //gambar titik
		} while (y < yend);
	}
	else if ((dy == 0) && (x1>x2)) {
		do {
			x += x_inc; // x = x + x_inc
			y += y_inc; // y = y + y_inc
			glVertex2i(round(x), round(y)); //gambar titik
		} while (x < xend);
	}
	else if ((dx == 0) && (y1>y2)) {
		do {
			x += x_inc; // x = x + x_inc
			y += y_inc; // y = y + y_inc
			glVertex2i(round(x), round(y)); //gambar titik
		} while (y < yend);
	}
	else {
		do {
			x += x_inc; // x = x + x_inc
			y += y_inc; // y = y + y_inc
			glVertex2i(round(x), round(y)); //gambar titik
		} while (x<xend);
	}
	


	glEnd();
	glFlush();
}

