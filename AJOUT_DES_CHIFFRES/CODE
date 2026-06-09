/* USER CODE BEGIN Header */
/**
  ******************************************************************************
  * @file           : main.c
  * @brief          : Main program body
  ******************************************************************************
  * @attention
  *
  * Copyright (c) 2026 STMicroelectronics.
  * All rights reserved.
  *
  * This software is licensed under terms that can be found in the LICENSE file
  * in the root directory of this software component.
  * If no LICENSE file comes with this software, it is provided AS-IS.
  *
  ******************************************************************************
  */
/* USER CODE END Header */
/* Includes ------------------------------------------------------------------*/
#include "main.h"
#include <string.h>
#include <stdio.h>
/* Private includes ----------------------------------------------------------*/
/* USER CODE BEGIN Includes */

/* USER CODE END Includes */

/* Private typedef -----------------------------------------------------------*/
/* USER CODE BEGIN PTD */

/* USER CODE END PTD */

/* Private define ------------------------------------------------------------*/
/* USER CODE BEGIN PD */

/* USER CODE END PD */

/* Private macro -------------------------------------------------------------*/
/* USER CODE BEGIN PM */

/* USER CODE END PM */

/* Private variables ---------------------------------------------------------*/
UART_HandleTypeDef huart1;

/* USER CODE BEGIN PV */
float currentX = 3.00;
float currentY = 10.50;
/* USER CODE END PV */

/* Private function prototypes -----------------------------------------------*/
void SystemClock_Config(void);
static void MX_GPIO_Init(void);
static void MX_USART1_UART_Init(void);
/* USER CODE BEGIN PFP */
void sendGcode(char *cmd);
void movePoint(float x, float y);
void hitMagnet(void);
void spaceBraille(void);
void newLine(void);
void ejectPaper(void);
void print_A(void);
void print_B(void);
void print_C(void);
void print_D(void);
void print_E(void);
void print_F(void);
void print_G(void);
void print_H(void);
void print_I(void);
void print_J(void);

void print_K(void);
void print_L(void);
void print_M(void);
void print_N(void);
void print_O(void);
void print_P(void);
void print_Q(void);
void print_R(void);
void print_S(void);
void print_T(void);
void print_U(void);
void print_V(void);
void print_W(void);
void print_X(void);
void print_Y(void);
void print_Z(void);
void vergule(void);
void print_interrogation(void);
void print_exclamation(void);
void print_DOT(void);
void print_COLON(void);
void print_COMMA(void);
void print_NUMBER_PREFIX(void);
/* USER CODE END PFP */

/* Private user code ---------------------------------------------------------*/
/* USER CODE BEGIN 0 */

/* USER CODE END 0 */

/**
  * @brief  The application entry point.
  * @retval int
  */
int main(void)
{

  /* USER CODE BEGIN 1 */

  /* USER CODE END 1 */

  /* MCU Configuration--------------------------------------------------------*/

  /* Reset of all peripherals, Initializes the Flash interface and the Systick. */
  HAL_Init();

  /* USER CODE BEGIN Init */

  /* USER CODE END Init */

  /* Configure the system clock */
  SystemClock_Config();

  /* USER CODE BEGIN SysInit */

  /* USER CODE END SysInit */

  /* Initialize all configured peripherals */
  MX_GPIO_Init();
  MX_USART1_UART_Init();
  sendGcode("G28 X");     // initialise X
  sendGcode("G28 Y");     // initialise Y
  sendGcode("G1 F4000");  // règle la vitesse
  /* USER CODE BEGIN 2 */

  /* USER CODE END 2 */

  /* Infinite loop */
  /* USER CODE BEGIN WHILE */
  while (1)
  {
      int b1 = (HAL_GPIO_ReadPin(GPIOA, GPIO_PIN_0) == GPIO_PIN_RESET);
      int b2 = (HAL_GPIO_ReadPin(GPIOA, GPIO_PIN_1) == GPIO_PIN_RESET);
      int b3 = (HAL_GPIO_ReadPin(GPIOB, GPIO_PIN_0) == GPIO_PIN_RESET);
      int b4 = (HAL_GPIO_ReadPin(GPIOB, GPIO_PIN_1) == GPIO_PIN_RESET);
      int b5 = (HAL_GPIO_ReadPin(GPIOB, GPIO_PIN_2) == GPIO_PIN_RESET);
      int b6 = (HAL_GPIO_ReadPin(GPIOB, GPIO_PIN_10) == GPIO_PIN_RESET);
      int retour = (HAL_GPIO_ReadPin(GPIOB, GPIO_PIN_11) == GPIO_PIN_RESET);
      int space = (HAL_GPIO_ReadPin(GPIOB, GPIO_PIN_12) == GPIO_PIN_RESET);
      int numero = (HAL_GPIO_ReadPin(GPIOB, GPIO_PIN_13) == GPIO_PIN_RESET);

      if (b1 || b2 || b3|| b4|| b5|| b6|| retour|| space || numero)
      {
          HAL_Delay(1000);

          b1 = (HAL_GPIO_ReadPin(GPIOA, GPIO_PIN_0) == GPIO_PIN_RESET);
          b2 = (HAL_GPIO_ReadPin(GPIOA, GPIO_PIN_1) == GPIO_PIN_RESET);
          b3 = (HAL_GPIO_ReadPin(GPIOB, GPIO_PIN_0) == GPIO_PIN_RESET);
          b4 = (HAL_GPIO_ReadPin(GPIOB, GPIO_PIN_1) == GPIO_PIN_RESET);
          b5 = (HAL_GPIO_ReadPin(GPIOB, GPIO_PIN_2) == GPIO_PIN_RESET);
          b6 = (HAL_GPIO_ReadPin(GPIOB, GPIO_PIN_10) == GPIO_PIN_RESET);
          retour = (HAL_GPIO_ReadPin(GPIOB, GPIO_PIN_11) == GPIO_PIN_RESET);
          space = (HAL_GPIO_ReadPin(GPIOB, GPIO_PIN_12) == GPIO_PIN_RESET);
          numero = (HAL_GPIO_ReadPin(GPIOB, GPIO_PIN_13) == GPIO_PIN_RESET);

          // Retour + Space = sortie feuille
          if (retour && space)
              ejectPaper();

          // Retour ligne seul
          else if (retour)
              newLine();

          // Espace seul
          else if (space)
              spaceBraille();

          // ================= MODE CHIFFRES =================
          // En Braille, les chiffres utilisent l'indicateur numérique
          // suivi des lettres A à J : A=1, B=2, C=3, D=4, E=5,
          // F=6, G=7, H=8, I=9, J=0.
          else if (numero && b1 && !b2 && !b3 && !b4 && !b5 && !b6)
          {
              print_NUMBER_PREFIX();
              print_A();   // 1
          }
          else if (numero && b1 && b2 && !b3 && !b4 && !b5 && !b6)
          {
              print_NUMBER_PREFIX();
              print_B();   // 2
          }
          else if (numero && b1 && !b2 && !b3 && b4 && !b5 && !b6)
          {
              print_NUMBER_PREFIX();
              print_C();   // 3
          }
          else if (numero && b1 && !b2 && !b3 && b4 && b5 && !b6)
          {
              print_NUMBER_PREFIX();
              print_D();   // 4
          }
          else if (numero && b1 && !b2 && !b3 && !b4 && b5 && !b6)
          {
              print_NUMBER_PREFIX();
              print_E();   // 5
          }
          else if (numero && b1 && b2 && !b3 && b4 && !b5 && !b6)
          {
              print_NUMBER_PREFIX();
              print_F();   // 6
          }
          else if (numero && b1 && b2 && !b3 && b4 && b5 && !b6)
          {
              print_NUMBER_PREFIX();
              print_G();   // 7
          }
          else if (numero && b1 && b2 && !b3 && !b4 && b5 && !b6)
          {
              print_NUMBER_PREFIX();
              print_H();   // 8
          }
          else if (numero && !b1 && b2 && !b3 && b4 && !b5 && !b6)
          {
              print_NUMBER_PREFIX();
              print_I();   // 9
          }
          else if (numero && !b1 && b2 && !b3 && b4 && b5 && !b6)
          {
              print_NUMBER_PREFIX();
              print_J();   // 0
          }

          // A = point 1
          else if (b1 && !b2 && !b3 && !b4 && !b5 && !b6)
              print_A();

          // B = points 1 2
          else if (b1 && b2 && !b3 && !b4 && !b5 && !b6)
              print_B();

          // C = points 1 4
          else if (b1 && !b2 && !b3 && b4 && !b5 && !b6)
              print_C();

          // D = points 1 4 5
          else if (b1 && !b2 && !b3 && b4 && b5 && !b6)
              print_D();

          // E = points 1 5
          else if (b1 && !b2 && !b3 && !b4 && b5 && !b6)
              print_E();

          // F = points 1 2 4
          else if (b1 && b2 && !b3 && b4 && !b5 && !b6)
              print_F();

          // G = points 1 2 4 5
          else if (b1 && b2 && !b3 && b4 && b5 && !b6)
              print_G();

          // H = points 1 2 5
          else if (b1 && b2 && !b3 && !b4 && b5 && !b6)
              print_H();

          // I = points 2 4
          else if (!b1 && b2 && !b3 && b4 && !b5 && !b6)
              print_I();

          // J = points 2 4 5
          else if (!b1 && b2 && !b3 && b4 && b5 && !b6)
              print_J();

          // K = points 1 3
          else if (b1 && !b2 && b3 && !b4 && !b5 && !b6)
              print_K();

          // L = points 1 2 3
          else if (b1 && b2 && b3 && !b4 && !b5 && !b6)
              print_L();

          // M = points 1 3 4
          else if (b1 && !b2 && b3 && b4 && !b5 && !b6)
              print_M();

          // N = points 1 3 4 5
          else if (b1 && !b2 && b3 && b4 && b5 && !b6)
              print_N();

          // O = points 1 3 5
          else if (b1 && !b2 && b3 && !b4 && b5 && !b6)
              print_O();

          // P = points 1 2 3 4
          else if (b1 && b2 && b3 && b4 && !b5 && !b6)
              print_P();

          // Q = points 1 2 3 4 5
          else if (b1 && b2 && b3 && b4 && b5 && !b6)
              print_Q();

          // R = points 1 2 3 5
          else if (b1 && b2 && b3 && !b4 && b5 && !b6)
              print_R();

          // S = points 2 3 4
          else if (!b1 && b2 && b3 && b4 && !b5 && !b6)
              print_S();

          // T = points 2 3 4 5
          else if (!b1 && b2 && b3 && b4 && b5 && !b6)
              print_T();

          // U = points 1 3 6
          else if (b1 && !b2 && b3 && !b4 && !b5 && b6)
              print_U();

          // V = points 1 2 3 6
          else if (b1 && b2 && b3 && !b4 && !b5 && b6)
              print_V();

          // W = points 2 4 5 6
          else if (!b1 && b2 && !b3 && b4 && b5 && b6)
              print_W();

          // X = points 1 3 4 6
          else if (b1 && !b2 && b3 && b4 && !b5 && b6)
              print_X();

          // Y = points 1 3 4 5 6
          else if (b1 && !b2 && b3 && b4 && b5 && b6)
              print_Y();

          // Z = points 1 3 5 6
          else if (b1 && !b2 && b3 && !b4 && b5 && b6)
              print_Z();
          // , = point 2

          else if (!b1 && b2 && !b3 && !b4 && !b5 && !b6)
              print_COMMA();

          // : = points 2 5
          else if (!b1 && b2 && !b3 && !b4 && b5 && !b6)
              print_COLON();

          // . = points 2 5 6
          else if (!b1 && b2 && !b3 && !b4 && b5 && b6)
              print_DOT();

          // ? = points 2 3 6
          else if (!b1 && b2 && b3 && !b4 && !b5 && b6)
              print_interrogation();

          // ! = points 2 3 5
          else if (!b1 && b2 && b3 && !b4 && b5 && !b6)
              print_exclamation();
          while (HAL_GPIO_ReadPin(GPIOA, GPIO_PIN_0) == GPIO_PIN_RESET ||
                 HAL_GPIO_ReadPin(GPIOA, GPIO_PIN_1) == GPIO_PIN_RESET ||
                 HAL_GPIO_ReadPin(GPIOB, GPIO_PIN_0) == GPIO_PIN_RESET ||
                 HAL_GPIO_ReadPin(GPIOB, GPIO_PIN_1) == GPIO_PIN_RESET||
                 HAL_GPIO_ReadPin(GPIOB, GPIO_PIN_2) == GPIO_PIN_RESET||
                 HAL_GPIO_ReadPin(GPIOB, GPIO_PIN_10) == GPIO_PIN_RESET||
                 HAL_GPIO_ReadPin(GPIOB, GPIO_PIN_11) == GPIO_PIN_RESET||
                 HAL_GPIO_ReadPin(GPIOB, GPIO_PIN_12) == GPIO_PIN_RESET||
                 HAL_GPIO_ReadPin(GPIOB, GPIO_PIN_13) == GPIO_PIN_RESET);


          HAL_Delay(100);
      }
  }
    /* USER CODE END WHILE */

    /* USER CODE BEGIN 3 */

  /* USER CODE END 3 */
}

/**
  * @brief System Clock Configuration
  * @retval None
  */
void SystemClock_Config(void)
{
  RCC_OscInitTypeDef RCC_OscInitStruct = {0};
  RCC_ClkInitTypeDef RCC_ClkInitStruct = {0};
  RCC_PeriphCLKInitTypeDef PeriphClkInit = {0};

  /** Initializes the RCC Oscillators according to the specified parameters
  * in the RCC_OscInitTypeDef structure.
  */
  RCC_OscInitStruct.OscillatorType = RCC_OSCILLATORTYPE_HSI;
  RCC_OscInitStruct.HSIState = RCC_HSI_ON;
  RCC_OscInitStruct.HSICalibrationValue = RCC_HSICALIBRATION_DEFAULT;
  RCC_OscInitStruct.PLL.PLLState = RCC_PLL_ON;
  RCC_OscInitStruct.PLL.PLLSource = RCC_PLLSOURCE_HSI;
  RCC_OscInitStruct.PLL.PLLMUL = RCC_PLL_MUL9;
  RCC_OscInitStruct.PLL.PREDIV = RCC_PREDIV_DIV1;
  if (HAL_RCC_OscConfig(&RCC_OscInitStruct) != HAL_OK)
  {
    Error_Handler();
  }

  /** Initializes the CPU, AHB and APB buses clocks
  */
  RCC_ClkInitStruct.ClockType = RCC_CLOCKTYPE_HCLK|RCC_CLOCKTYPE_SYSCLK
                              |RCC_CLOCKTYPE_PCLK1|RCC_CLOCKTYPE_PCLK2;
  RCC_ClkInitStruct.SYSCLKSource = RCC_SYSCLKSOURCE_PLLCLK;
  RCC_ClkInitStruct.AHBCLKDivider = RCC_SYSCLK_DIV1;
  RCC_ClkInitStruct.APB1CLKDivider = RCC_HCLK_DIV2;
  RCC_ClkInitStruct.APB2CLKDivider = RCC_HCLK_DIV1;

  if (HAL_RCC_ClockConfig(&RCC_ClkInitStruct, FLASH_LATENCY_2) != HAL_OK)
  {
    Error_Handler();
  }
  PeriphClkInit.PeriphClockSelection = RCC_PERIPHCLK_USART1;
  PeriphClkInit.Usart1ClockSelection = RCC_USART1CLKSOURCE_PCLK2;
  if (HAL_RCCEx_PeriphCLKConfig(&PeriphClkInit) != HAL_OK)
  {
    Error_Handler();
  }
}

/**
  * @brief USART1 Initialization Function
  * @param None
  * @retval None
  */
static void MX_USART1_UART_Init(void)
{

  /* USER CODE BEGIN USART1_Init 0 */

  /* USER CODE END USART1_Init 0 */

  /* USER CODE BEGIN USART1_Init 1 */

  /* USER CODE END USART1_Init 1 */
  huart1.Instance = USART1;
  huart1.Init.BaudRate = 250000;
  huart1.Init.WordLength = UART_WORDLENGTH_8B;
  huart1.Init.StopBits = UART_STOPBITS_1;
  huart1.Init.Parity = UART_PARITY_NONE;
  huart1.Init.Mode = UART_MODE_TX_RX;
  huart1.Init.HwFlowCtl = UART_HWCONTROL_NONE;
  huart1.Init.OverSampling = UART_OVERSAMPLING_16;
  huart1.Init.OneBitSampling = UART_ONE_BIT_SAMPLE_DISABLE;
  huart1.AdvancedInit.AdvFeatureInit = UART_ADVFEATURE_NO_INIT;
  if (HAL_UART_Init(&huart1) != HAL_OK)
  {
    Error_Handler();
  }
  /* USER CODE BEGIN USART1_Init 2 */

  /* USER CODE END USART1_Init 2 */

}

/**
  * @brief GPIO Initialization Function
  * @param None
  * @retval None
  */
static void MX_GPIO_Init(void)
{
  GPIO_InitTypeDef GPIO_InitStruct = {0};
/* USER CODE BEGIN MX_GPIO_Init_1 */
/* USER CODE END MX_GPIO_Init_1 */

  /* GPIO Ports Clock Enable */
  __HAL_RCC_GPIOA_CLK_ENABLE();
  __HAL_RCC_GPIOC_CLK_ENABLE();
  __HAL_RCC_GPIOB_CLK_ENABLE();

  /*Configure GPIO pins : PA0 PA1 */
  GPIO_InitStruct.Pin = GPIO_PIN_0|GPIO_PIN_1;
  GPIO_InitStruct.Mode = GPIO_MODE_INPUT;
  GPIO_InitStruct.Pull = GPIO_PULLUP;
  HAL_GPIO_Init(GPIOA, &GPIO_InitStruct);

  /*Configure GPIO pins : PB0 PB1 PB2 PB10
                           PB11 PB12 PB13 */
  GPIO_InitStruct.Pin = GPIO_PIN_0|GPIO_PIN_1|GPIO_PIN_2|GPIO_PIN_10
                          |GPIO_PIN_11|GPIO_PIN_12|GPIO_PIN_13;
  GPIO_InitStruct.Mode = GPIO_MODE_INPUT;
  GPIO_InitStruct.Pull = GPIO_PULLUP;
  HAL_GPIO_Init(GPIOB, &GPIO_InitStruct);

/* USER CODE BEGIN MX_GPIO_Init_2 */
/* USER CODE END MX_GPIO_Init_2 */
}

/* USER CODE BEGIN 4 */
void sendGcode(char *cmd)
{
  HAL_UART_Transmit(&huart1,
                    (uint8_t*)cmd,
                    strlen(cmd),
                    HAL_MAX_DELAY);

  HAL_UART_Transmit(&huart1,
                    (uint8_t*)"\r\n",
                    2,
                    HAL_MAX_DELAY);

  HAL_Delay(100);
}
void spaceBraille(void)
{
  currentX += 12.10;
  movePoint(currentX, currentY);// espace = une cellule vide
}

void newLine(void)
{
  currentX = 3.00;     // retour début ligne
  currentY += 9.90;  // ligne suivante
  movePoint(currentX, currentY);
}
void ejectPaper(void)
{
    sendGcode("G91");              // mode relatif
    sendGcode("G1 Y270 F3000");   // sortie feuille en arrière
    sendGcode("M400");
    sendGcode("G90");              // retour mode absolu

    currentX = 3.00;
    currentY = 10.50;
}
void movePoint(float x, float y)
{
  char cmd[50];

  sprintf(cmd,"G1 X%.2f Y%.2f F4000", x, y);
  sendGcode(cmd);

  HAL_Delay(200);

  sendGcode("M400");
}

void hitMagnet(void)
{
  sendGcode("M3 S255");

  HAL_Delay(500);

  sendGcode("M3 S0");

  HAL_Delay(300);
}
void printDot(float dx, float dy)
{
    movePoint(currentX + dx, currentY + dy);
    hitMagnet();
}
void nextLetter(void)
{
    currentX += 6.05;
    // revenir à la position principale de la ligne

}

// ================= A =================
void print_A(void)
{
    movePoint(currentX, currentY);
    hitMagnet();

    currentX += 6.05;
}

// ================= B =================

void print_B(void)
{
    // point 1
    movePoint(currentX, currentY);
    hitMagnet();

    // point 2
    movePoint(currentX, currentY + 5.00);
    hitMagnet();

    // retour à la position de base
    movePoint(currentX, currentY);

    // lettre suivante
    currentX += 6.05;
}
// ================= C =================
void print_C(void)
{
    printDot(0.00, 0.00);
    printDot(2.30, 0.00);
    movePoint(currentX, currentY);
    nextLetter();
}

// ================= D =================
void print_D(void)
{
    movePoint(currentX, currentY);
    hitMagnet();

    movePoint(currentX + 2.30, currentY);
    hitMagnet();

    movePoint(currentX + 2.30, currentY + 5.00);
    hitMagnet();

    movePoint(currentX, currentY);
    currentX += 6.05;
}


// ================= E =================
void print_E(void)
{
    movePoint(currentX, currentY);
    hitMagnet();

    movePoint(currentX + 2.30, currentY + 5.00);
    hitMagnet();

    movePoint(currentX, currentY);
    currentX += 6.05;
}

// ================= F =================
void print_F(void)
{
    movePoint(currentX, currentY);
    hitMagnet();

    movePoint(currentX, currentY + 5.00);
    hitMagnet();

    movePoint(currentX + 2.30, currentY);
    hitMagnet();

    movePoint(currentX, currentY);
    currentX += 6.05;
}

// ================= G =================
void print_G(void)
{
    movePoint(currentX, currentY);
    hitMagnet();

    movePoint(currentX, currentY + 5.00);
    hitMagnet();

    movePoint(currentX + 2.30, currentY);
    hitMagnet();

    movePoint(currentX + 2.30, currentY + 5.00);
    hitMagnet();

    movePoint(currentX, currentY);
    currentX += 6.05;
}

// ================= H =================
void print_H(void)
{
    movePoint(currentX, currentY);
    hitMagnet();

    movePoint(currentX, currentY + 5.00);
    hitMagnet();

    movePoint(currentX + 2.30, currentY + 5.00);
    hitMagnet();

    movePoint(currentX, currentY);
    currentX += 6.05;
}

// ================= I =================
void print_I(void)
{
    movePoint(currentX, currentY + 5.00);
    hitMagnet();

    movePoint(currentX + 2.30, currentY);
    hitMagnet();

    movePoint(currentX, currentY);
    currentX += 6.05;
}

// ================= J =================
void print_J(void)
{
    movePoint(currentX, currentY + 5.00);
    hitMagnet();

    movePoint(currentX + 2.30, currentY);
    hitMagnet();

    movePoint(currentX + 2.30, currentY + 5.00);
    hitMagnet();

    movePoint(currentX, currentY);
    currentX += 6.05;
}

// ================= K =================
void print_K(void)
{
    movePoint(currentX, currentY);
    hitMagnet();

    HAL_Delay(1000);

    movePoint(currentX, currentY + 6.70);
    hitMagnet();

    movePoint(currentX, currentY);
    currentX += 6.05;
}

// ================= L =================
void print_L(void)
{
    // point 1
    movePoint(currentX, currentY);
    hitMagnet();

    HAL_Delay(500);

    // point 2
    movePoint(currentX, currentY + 5.00);
    hitMagnet();

    HAL_Delay(500);

    // point 3
    movePoint(currentX, currentY + 6.70);
    hitMagnet();

    // retour au niveau de base
    movePoint(currentX, currentY);

    // lettre suivante
    currentX += 6.05;
}

// ================= M =================
void print_M(void)
{
    movePoint(currentX, currentY);
    hitMagnet();

    movePoint(currentX, currentY + 6.70);
    hitMagnet();

    movePoint(currentX + 2.30, currentY);
    hitMagnet();

    movePoint(currentX, currentY);
    currentX += 6.05;
}

// ================= N =================
void print_N(void)
{
    movePoint(currentX, currentY);
    hitMagnet();

    movePoint(currentX, currentY + 6.70);
    hitMagnet();

    movePoint(currentX + 2.30, currentY);
    hitMagnet();

    movePoint(currentX + 2.30, currentY + 5.00);
    hitMagnet();

    movePoint(currentX, currentY);
    currentX += 6.05;
}

// ================= O =================
void print_O(void)
{
    movePoint(currentX, currentY);
    hitMagnet();

    movePoint(currentX, currentY + 6.70);
    hitMagnet();

    movePoint(currentX + 2.30, currentY + 5.00);
    hitMagnet();

    movePoint(currentX, currentY);
    currentX += 6.05;
}

// ================= P =================
void print_P(void)
{
    movePoint(currentX, currentY);
    hitMagnet();

    movePoint(currentX, currentY + 5.00);
    hitMagnet();

    movePoint(currentX, currentY + 6.70);
    hitMagnet();

    movePoint(currentX + 2.30, currentY);
    hitMagnet();

    movePoint(currentX, currentY);
    currentX += 6.05;
}

// ================= Q =================
void print_Q(void)
{
    movePoint(currentX, currentY);
    hitMagnet();

    movePoint(currentX, currentY + 5.00);
    hitMagnet();

    movePoint(currentX, currentY + 6.70);
    hitMagnet();

    movePoint(currentX + 2.30, currentY);
    hitMagnet();

    movePoint(currentX + 2.30, currentY + 5.00);
    hitMagnet();

    movePoint(currentX, currentY);
    currentX += 6.05;
}

// ================= R =================
void print_R(void)
{
    movePoint(currentX, currentY);
    hitMagnet();

    movePoint(currentX, currentY + 5.00);
    hitMagnet();

    movePoint(currentX, currentY + 6.70);
    hitMagnet();

    movePoint(currentX + 2.30, currentY + 5.00);
    hitMagnet();

    movePoint(currentX, currentY);
    currentX += 6.05;
}

// ================= S =================
void print_S(void)
{
    movePoint(currentX, currentY + 5.00);
    hitMagnet();

    movePoint(currentX, currentY + 6.70);
    hitMagnet();

    movePoint(currentX + 2.30, currentY);
    hitMagnet();

    movePoint(currentX, currentY);
    currentX += 6.05;
}
// ================= T =================
void print_T(void)
{
    movePoint(currentX, currentY + 5.00);
    hitMagnet();

    movePoint(currentX, currentY + 6.70);
    hitMagnet();

    movePoint(currentX + 2.30, currentY);
    hitMagnet();

    movePoint(currentX + 2.30, currentY + 5.00);
    hitMagnet();

    movePoint(currentX, currentY);
    currentX += 6.05;
}
// ================= U =================
void print_U(void)
{
    movePoint(currentX, currentY);
    hitMagnet();

    movePoint(currentX, currentY + 6.70);
    hitMagnet();

    movePoint(currentX + 2.30, currentY + 6.70);
    hitMagnet();

    movePoint(currentX, currentY);
    currentX += 6.05;
}

// ================= V =================
void print_V(void)
{
    movePoint(currentX, currentY);
    hitMagnet();

    movePoint(currentX, currentY + 5.00);
    hitMagnet();

    movePoint(currentX, currentY + 6.70);
    hitMagnet();

    movePoint(currentX + 2.30, currentY + 6.70);
    hitMagnet();

    movePoint(currentX, currentY);
    currentX += 6.05;
}

// ================= W =================
void print_W(void)
{
    movePoint(currentX, currentY + 5.00);
    hitMagnet();

    movePoint(currentX + 2.30, currentY);
    hitMagnet();

    movePoint(currentX + 2.30, currentY + 5.00);
    hitMagnet();

    movePoint(currentX + 2.30, currentY + 6.70);
    hitMagnet();

    movePoint(currentX, currentY);
    currentX += 6.05;
}

// ================= X =================
void print_X(void)
{
    movePoint(currentX, currentY);
    hitMagnet();

    movePoint(currentX, currentY + 6.70);
    hitMagnet();

    movePoint(currentX + 2.30, currentY);
    hitMagnet();

    movePoint(currentX + 2.30, currentY + 6.70);
    hitMagnet();

    movePoint(currentX, currentY);
    currentX += 6.05;
}

// ================= Y  =================
void print_Y(void)
{
    movePoint(currentX, currentY);
    hitMagnet();

    movePoint(currentX, currentY + 6.70);
    hitMagnet();

    movePoint(currentX + 2.30, currentY);
    hitMagnet();

    movePoint(currentX + 2.30, currentY + 5.00);
    hitMagnet();

    movePoint(currentX + 2.30, currentY + 6.70);
    hitMagnet();

    movePoint(currentX, currentY);
    currentX += 6.05;
}

// ================= Z =================
void print_Z(void)
{
    movePoint(currentX, currentY);
    hitMagnet();

    movePoint(currentX, currentY + 6.70);
    hitMagnet();

    movePoint(currentX + 2.30, currentY + 5.00);
    hitMagnet();

    movePoint(currentX + 2.30, currentY + 6.70);
    hitMagnet();

    movePoint(currentX, currentY);
    currentX += 6.05;
}
// ================= POINT (.) =================
void print_DOT(void)
{
    movePoint(currentX, currentY + 5.00);
    hitMagnet();

    movePoint(currentX + 2.30, currentY + 5.00);
    hitMagnet();

    movePoint(currentX + 2.30, currentY + 6.70);
    hitMagnet();

    movePoint(currentX, currentY);
    currentX += 6.05;
}
// ================= VIRGULE (,)  =================
void print_COMMA(void)
{
    movePoint(currentX, currentY + 5.00);
    hitMagnet();

    movePoint(currentX, currentY);
    currentX += 6.05;
}
// ================= DEUX-POINTS (:)  =================
void print_COLON(void)
{
    movePoint(currentX, currentY + 5.00);
    hitMagnet();

    movePoint(currentX + 2.30, currentY + 5.00);
    hitMagnet();

    movePoint(currentX, currentY);
    currentX += 6.05;
}
void print_interrogation(void)
{
    movePoint(currentX, currentY + 5.00);
    hitMagnet();

    movePoint(currentX, currentY + 6.70);
    hitMagnet();

    movePoint(currentX + 2.30, currentY + 6.70);
    hitMagnet();

    movePoint(currentX, currentY);
    currentX += 6.05;
}
void print_exclamation(void)
{
    movePoint(currentX, currentY + 5.00);
    hitMagnet();

    movePoint(currentX, currentY + 6.70);
    hitMagnet();

    movePoint(currentX + 2.30, currentY + 5.00);
    hitMagnet();

    movePoint(currentX, currentY);
    currentX += 6.05;
}
// ================= INDICATEUR NUMERIQUE =================
void print_NUMBER_PREFIX(void)
{
    // Indicateur numérique Braille = points 3 4 5 6
    // Il est imprimé avant les lettres A à J pour former les chiffres.

    printDot(0.00, 6.70);  // point 3
    printDot(2.30, 0.00);  // point 4
    printDot(2.30, 5.00);  // point 5
    printDot(2.30, 6.70);  // point 6

    movePoint(currentX, currentY);
    nextLetter();
}

/* USER CODE END 4 */

/**
  * @brief  This function is executed in case of error occurrence.
  * @retval None
  */
void Error_Handler(void)
{
  /* USER CODE BEGIN Error_Handler_Debug */
  /* User can add his own implementation to report the HAL error return state */
  __disable_irq();
  while (1)
  {
  }
  /* USER CODE END Error_Handler_Debug */
}

#ifdef  USE_FULL_ASSERT
/**
  * @brief  Reports the name of the source file and the source line number
  *         where the assert_param error has occurred.
  * @param  file: pointer to the source file name
  * @param  line: assert_param error line source number
  * @retval None
  */
void assert_failed(uint8_t *file, uint32_t line)
{
  /* USER CODE BEGIN 6 */
  /* User can add his own implementation to report the file name and line number,
     ex: printf("Wrong parameters value: file %s on line %d\r\n", file, line) */
  /* USER CODE END 6 */
}
#endif /* USE_FULL_ASSERT */
