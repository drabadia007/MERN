# MERN

## code to connect to the mongo db database
module.exports = () => {
  const connectionParams = {
    useNewUrlParser: true,
    useUnifiedTopology: true,
  };

  try {
    mongoose.connect(process.env.MONGO_URL, connectionParams);
    console.log("connected to DB successfully");
  } catch (error) {
    console.log(error);
    console.log("error occured while connecting to the DB");
  }
};
