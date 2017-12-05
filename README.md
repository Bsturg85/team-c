# team-c
sorter code
clear;
port = '/dev/cu.usbmodem1421';
board = 'uno';
 
a = arduino(port,board);
 
s1 = servo(a, 'D10', 'MinPulseDuration', 900 *10^-6, 'MaxPulseDuration', 2300*10^-6);
% pause(0.5);
s2 = servo(a, 'D9', 'MinPulseDuration', 900*10^-6, 'MaxPulseDuration', 2600*10^-6);
% pause(0.5);
s3 = servo(a, 'D11', 'MinPulseDuration', 900*10^-6, 'MaxPulseDuration', 2600*10^-6);
% pause(0.5);
analog=zeros(1,50);
 
for x = 1:5
    
    pause(2);
    writePosition(s1,0);
    pause(0.5);
    writePosition(s1,0.5);
    pause(2);
% %     writePosition(s1,1);
% %     pause(0.8);
% %     writePosition(s1,.25);
% %     pause(1);
% %     writePosition(s1,1);
% %     pause(1);
% %     writePosition(s1,0);
%     
% %     angle = .5;     
% %     writePosition(s2,angle);
% 
    pause(0.3);
    reading = 0;
    AllValues = 0;
    pause(0.8);
    for index = 1:50
        analog(index) = readVoltage(a, 'A0');
        reading = readVoltage(a, 'A0');
        fprintf('%.4f', reading);
        AllValues = reading + AllValues;
        pause(0.2);
    end
    
    AveValues = AllValues/50;
    fprintf('\nAverage = %.4f \n', AveValues);
    pause(0.8);
    
   
    if AveValues >= 3.0
        pause(0.8);
        writePosition(s3,1);
        pause(3);
    
    elseif (AveValues >= 2.05) && (AveValues < 2.5)
        pause(0.8);
        writePosition(s3,0.8);
        pause(3);
    
    elseif (AveValues >= 1.7) && (AveValues < 2.05)
        pause(0.8);
        writePosition(s3,0.6);
        pause(3);
   
    elseif (AveValues >= 0.5) && (AveValues < 0.9)
        pause(0.8);
        writePosition(s3,0.4);
        pause(3);
    
    elseif (AveValues >= 0.2) && (AveValues < 0.5)
        pause(0.8);
        writePosition(s3,0.2);
        pause(3);
%     elseif AveValues >= 0.05
%         writePosition(s3,1.0);
%         pause(0.3);
    else 
        pause(0.8);
        writePosition(s3,0);
        pause(3);
    end
    
    pause(1);
    
    writePosition(s2,.5);
    pause(0.8);
    writePosition(s2,0);
    pause(2);
%     writePosition(s2,0.5);
    pause(5);
    
    
    
    
    
end
% 
