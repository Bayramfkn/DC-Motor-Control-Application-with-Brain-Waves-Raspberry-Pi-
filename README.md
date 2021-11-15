# Beyin-Dalgalar-ile-Motor-Kontrol-Kodu(Raspberry Pi)

import time
from mindwavemobile.MindwaveDataPoints import RawDataPoint
from mindwavemobile.MindwaveDataPointReader import MindwaveDataPointReader
from mindwavemobile.MindwaveDataPoints import MeditationDataPoint
from mindwavemobile.MindwaveDataPoints import AttentionDataPoint
import RPi.GPIO as GPIO
import bluetooth
import textwrap
GPIO.setwarnings(False)
GPIO.setmode(GPIO.BCM)
IN1R1 = 11
IN2R2 = 12
IN3L1= 13
IN4L2= 15

GPIO.setup(IN1R1,GPIO.OUT)
GPIO.setup(IN2R2,GPIO.OUT)
GPIO.setup(IN3L1,GPIO.OUT)
GPIO.setup(IN4L2,GPIO.OUT)
GPIO.setup(19,GPIO.OUT)
GPIO.setup(18,GPIO.OUT)

ea = GPIO.PWM(19,100)
ea.start(0)
eb = GPIO.PWM(18,100)
eb.start(0)

if __name__ == '__main__':
    mindwaveDataPointReader = MindwaveDataPointReader()
    mindwaveDataPointReader.start()
    if (mindwaveDataPointReader.isConnected()):    
        while(True):
            dataPoint = mindwaveDataPointReader.readNextDataPoint()
            if (not dataPoint.__class__ is RawDataPoint):
                if ( dataPoint.__class__ is MeditationDataPoint):
                    
                    if (dataPoint.meditationValue <=20  ):
                        ea.ChangeDutyCycle(0) 
                        eb.ChangeDutyCycle(0)
                        GPIO.output(IN1R1,GPIO.LOW)
                        GPIO.output(IN2R2,GPIO.LOW)
                        GPIO.output(IN3L1,GPIO.LOW)
                        GPIO.output(IN4L2,GPIO.LOW)
                    elif (dataPoint.meditationValue <=30  ):
                        ea.ChangeDutyCycle(10) 
                        eb.ChangeDutyCycle(10)
                        GPIO.output(IN1R1,GPIO.HIGH)
                        GPIO.output(IN2R2,GPIO.LOW)
                        GPIO.output(IN3L1,GPIO.HIGH)
                        GPIO.output(IN4L2,GPIO.LOW)
                    elif (dataPoint.meditationValue <=40  ):
                        ea.ChangeDutyCycle(20) 
                        eb.ChangeDutyCycle(20)
                        GPIO.output(IN1R1,GPIO.HIGH)
                        GPIO.output(IN2R2,GPIO.LOW)
                        GPIO.output(IN3L1,GPIO.HIGH)
                        GPIO.output(IN4L2,GPIO.LOW)
                    elif (dataPoint.meditationValue <=50):
                        ea.ChangeDutyCycle(30) 
                        eb.ChangeDutyCycle(30)
                        GPIO.output(IN1R1,GPIO.HIGH)
                        GPIO.output(IN2R2,GPIO.LOW)
                        GPIO.output(IN3L1,GPIO.HIGH)
                        GPIO.output(IN4L2,GPIO.LOW)
                    elif (dataPoint.meditationValue <=60  ):
                        ea.ChangeDutyCycle(40) 
                        eb.ChangeDutyCycle(40)
                        GPIO.output(IN1R1,GPIO.HIGH)
                        GPIO.output(IN2R2,GPIO.LOW)
                        GPIO.output(IN3L1,GPIO.HIGH)
                        GPIO.output(IN4L2,GPIO.LOW)
                    elif (dataPoint.meditationValue <=70  ):
                        ea.ChangeDutyCycle(50) 
                        eb.ChangeDutyCycle(50)
                        GPIO.output(IN1R1,GPIO.HIGH)
                        GPIO.output(IN2R2,GPIO.LOW)
                        GPIO.output(IN3L1,GPIO.HIGH)
                        GPIO.output(IN4L2,GPIO.LOW)
                    elif (dataPoint.meditationValue <= 80 ):
                        ea.ChangeDutyCycle(75) 
                        eb.ChangeDutyCycle(75)
                        GPIO.output(IN1R1,GPIO.HIGH)
                        GPIO.output(IN2R2,GPIO.LOW)
                        GPIO.output(IN3L1,GPIO.HIGH)
                        GPIO.output(IN4L2,GPIO.LOW)
                    elif (dataPoint.meditationValue <=90 ):
                        ea.ChangeDutyCycle(85) 
                        eb.ChangeDutyCycle(85)
                        GPIO.output(IN1R1,GPIO.HIGH)
                        GPIO.output(IN2R2,GPIO.LOW)
                        GPIO.output(IN3L1,GPIO.HIGH)
                        GPIO.output(IN4L2,GPIO.LOW)
                    elif (dataPoint.meditationValue <=100  ):
                        ea.ChangeDutyCycle(100) 
                        eb.ChangeDutyCycle(100)
                        GPIO.output(IN1R1,GPIO.HIGH)
                        GPIO.output(IN2R2,GPIO.LOW)
                        GPIO.output(IN3L1,GPIO.HIGH)
                        GPIO.output(IN4L2,GPIO.LOW)
                      
                    print("meditasyon : ",dataPoint.meditationValue )
                elif (dataPoint.__class__ is AttentionDataPoint):
                    print("dikkat : ",dataPoint.attentionValue)
                #else:
                    #print(dataPoint)
        
    
    else:
        print((textwrap.dedent("""\
            Exiting because the program could not connect
            to the Mindwave Mobile device.""").replace("\n", " ")))
        ea.stop() 
        eb.stop()
        


