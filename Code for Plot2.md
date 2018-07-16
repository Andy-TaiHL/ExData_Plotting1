##EXPLORATORY DATA ANALYSIS COURSE - R CODE FOR PLOT 2
getwd()
setwd("C:\\Users\\Andy's Home PC\\Documents\\Coursera Courses\\Data Science\\Exploratory Data Analysis\\Week 1")
getwd()


##1.  Reading Data from file and subsetting to specific dates
data<-read.table("household_power_consumption.txt", 
                 header = TRUE, 
                 sep = ";", 
                 colClasses = c("character","character", rep("numeric",7)), 
                 na.strings = "?")

data_sub<-subset(data,data$Date=="1/2/2007" | data$Date == "2/2/2007")


##2. converting data and time to specific format and assigning in to a new column"DateTime" 
data_sub$Date <- as.Date(data_sub$Date, format = "%d/%m/%Y")
data_sub$DateTime <- as.POSIXct(paste(data_sub$Date, data_sub$Time))
Sys.setlocale("LC_TIME", "English")


##3. Plot line graph (Plot2)
plot(data_sub$DateTime, data_sub$Global_active_power, 
     type="line", 
     xlab="", 
     ylab="Global Active Power (kilowatts)")

## Save file as png in wd
dev.copy(png, file="plot2.png", width = 480, height = 480)
dev.off
